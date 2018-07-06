---
uid: web-pages/overview/data/5-working-with-data
title: 使用 ASP.NET Web 中的数据库简介页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 此章节介绍了如何从数据库访问数据并显示它使用 ASP.NET Web Pages。
ms.author: aspnetcontent
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 5185769530cf78c301f2ac43b25dba6e77ca75a2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808501"
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>使用 ASP.NET Web 中的数据库简介页 (Razor) 站点
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 Microsoft WebMatrix 工具来创建一个数据库中的 ASP.NET Web Pages (Razor) 网站，以及如何创建网页，让你显示、 添加、 编辑和删除数据。
> 
> **你将学习：** 
> 
> - 如何创建数据库。
> - 如何连接到数据库。
> - 如何在网页中显示数据。
> - 如何插入、 更新和删除数据库记录。
> 
> 下面是在本文中引入的功能：
> 
> - 使用 Microsoft SQL Server Compact Edition 数据库。
> - 使用 SQL 查询。
> - `Database` 类。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。 可以使用 ASP.NET Web Pages 3 和 Visual Studio 2013 （或 Visual Studio Express 2013 for Web）;但是，用户界面将会不同。


## <a name="introduction-to-databases"></a>数据库简介

想象一下典型的通讯簿。 通讯簿中的每个项 (即，每个用户) 包含一些相关的信息，例如名字、 姓氏、 地址、 电子邮件地址和电话号码。

为此类的图片数据的典型方式是为包含行和列的表。 在数据库术语中，每个行是通常称为一条记录。 每个列 （有时称为字段） 包含每种类型的数据的值： 名字、 最后一个名称和等等。

| **ID** | **FirstName** | **姓氏** | **地址** | **电子邮件** | **电话** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210 100th St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St.西雅图华盛顿州 99011 | terry@cohowinery.com | 555 0101 |

对于大多数数据库表，该表必须具有包含唯一标识符，如客户编号、 帐号等的列。这就是表的*主键*，并使用它来标识表中的每个行。 在示例中，ID 列是主键的通讯簿。

此数据库的基本的了解，就可以了解如何创建一个简单的数据库并执行操作，如添加、 修改和删除数据。

> [!TIP] 
> 
> **关系数据库**
> 
> 可以在很多方面，包括文本文件和电子表格来存储数据。 对于大多数业务应用中，不过，数据存储在关系数据库中。
> 
> 本文不深入进入数据库。 但是，你可能会发现它可以了解一些有关它们。 在关系数据库中，信息在逻辑上划分成不同的表。 例如，一所学校的数据库可能包含不同的表，面向学生和类产品/服务。 软件 （如 SQL Server) 支持功能强大的数据库命令，允许动态建立表之间的关系。 例如，关系数据库可用于建立以创建计划的学生和类之间的逻辑关系。 在单独的表中存储数据缩短表结构的复杂性并减少冗余数据保留在表的需求。


## <a name="creating-a-database"></a>创建数据库

此过程演示如何创建一个名为 SmallBakery 通过使用在 WebMatrix 中包含的 SQL Server Compact 数据库设计工具。 尽管可以创建使用代码的数据库，但它是更常见的做法创建数据库和 WebMatrix 之类的设计工具的数据库表。

1. 启动 WebMatrix，然后在快速启动页上，单击**从模板**。
2. 选择**空站点**，然后在**站点名称**中输入"SmallBakery"，然后单击**确定**。 创建并显示在 WebMatrix 站点。
3. 在左窗格中，单击**数据库**工作区。
4. 在功能区中，单击**新的数据库**。 使用与你的站点相同的名称创建空数据库。
5. 在左窗格中，展开**SmallBakery.sdf**节点，然后单击**表**。
6. 在功能区中，单击**新表**。 WebMatrix 将打开表设计器。

    ![[image]](5-working-with-data/_static/image1.jpg)
7. 在单击**名称**列并输入&quot;Id&quot;。
8. 在中**数据类型**列中，选择**int**。
9. 设置**是主键？** 并**是标识？** 到选项**是**。

    顾名思义，**是 Primary Key**告诉数据库，这将是表的主键。 **是标识**告诉数据库自动创建新的每个记录的 ID 号，并将其分配给下一个序列号 （从 1 开始）。
10. 单击下一步的行。 编辑器中启动的新列定义。
11. 对于名称值中，输入&quot;名称&quot;。
12. 有关**数据类型**，选择&quot;nvarchar&quot;并将长度设置为 50。 *Var*属于`nvarchar`告诉数据库，此列的数据将一个字符串，其大小可能会记录到记录。 ( *N*前缀表示*国家/地区*，该值指示该字段可以容纳表示任何字母的字符数据或写入系统&#8212;，即该字段包含 Unicode 数据。)
13. 设置**允许 null 值**选项设为**否**。 这会强制此要求*名称*列不保留为空。
14. 使用此相同的过程中，创建名为的列*说明*。 设置**数据类型**为"nvarchar"和长度，并将设置 50**允许 null 值**为 false。
15. 创建名为的列*价格*。 设置**数据类型设置为"money"** 并设置**允许 null 值**为 false。
16. 在顶部框中，将表命名&quot;产品&quot;。

    完成后，定义将如下所示：

    ![[image]](5-working-with-data/_static/image2.jpg)
17. 按 Ctrl + S 保存该表。

## <a name="adding-data-to-the-database"></a>向数据库添加数据

现在可以将一些示例数据添加到您在本文的后面将使用的数据库。

1. 在左窗格中，展开**SmallBakery.sdf**节点，然后单击**表**。
2. 右键单击 Product 表，然后单击**数据**。
3. 在编辑窗格中，输入以下记录：

    | **名称** | **说明** | **价格** |
    | --- | --- | --- |
    | 面包 | 生成的全新每一天。 | 2.99 |
    | 草莓 Shortcake | 使用自然 strawberries 进行从我们园。 | 9.99 |
    | Apple 饼图 | 仅为你的妈妈饼图的第二个。 | 12.99 |
    | Pecan 饼图 | 如果您喜欢 pecans，这是用于您。 | 10.99 |
    | 柠檬饼图 | 使用世界上最佳柠檬进行。 | 11.99 |
    | Cupcakes | 自己的孩子和 kid 中您会喜欢这些。 | 7.99 |

    请记住，您不必输入的任何内容*Id*列。 在创建时*Id*列，设置其**是标识**属性设为 true，这会导致它自动填写。

    完成输入数据后，表设计器将如下所示：

    ![[image]](5-working-with-data/_static/image3.jpg)
4. 关闭包含数据库数据的选项卡。

## <a name="displaying-data-from-a-database"></a>显示数据库中的数据

一旦在其中配置了具有数据的数据库，您可以在 ASP.NET web 页中显示数据。 若要选择要显示的表行，您使用 SQL 语句，这是一个命令，将传递到数据库。

1. 在左窗格中，单击**文件**工作区。
2. 在该网站的根目录中创建一个名为的新 CSHTML 页*ListProducts.cshtml*。
3. 使用以下内容替换现有标记：

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    在第一个代码块中，打开*SmallBakery.sdf*前面创建的文件 （数据库）。 `Database.Open`方法假设 *.sdf*文件位于你的网站*应用\_数据*文件夹。 (请注意，无需指定 *.sdf*扩展&#8212;事实上，如果这样做，`Open`方法不起作用。)

    > [!NOTE]
    > *应用程序\_数据*文件夹是用于存储数据文件的 ASP.NET 中的特殊文件夹。 有关详细信息，请参阅[连接到数据库](#SB_ConnectingToADatabase)这篇文章中更高版本。

    然后发出请求，以查询使用下面的 SQL 数据库`Select`语句：

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    在语句中，`Product`标识查询的表。 `*`字符指定查询应返回表中的所有列。 （你可能还列出列单独，以逗号分隔，如果你想要查看仅某些列。）`Order By`子句指示数据的排序方式&#8212;在这种情况下，通过*名称*列。 这意味着对数据进行排序的值按字母顺序根据*名称*每个行的列。

    在页面的正文中，标记创建一个将用于显示数据的 HTML 表。 内部`<tbody>`元素，使用`foreach`循环，以便单独获取由查询返回每个数据行。 对于每个数据行，创建一个 HTML 表行 (`<tr>`元素)。 然后创建 HTML 表格单元格 (`<td>`元素) 的每个列。 每次执行循环，从数据库的下一个可用行处于`row`变量 (对此进行设置`foreach`语句)。 若要从行中获取的单个列，可以使用`row.Name`或`row.Description`或者的列的任何名称是你想要。
4. 在浏览器中运行页。 (请确保的页中选择**文件**工作区之前运行它。)页将显示如下所示列表：

    ![[image]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **结构化的查询语言 (SQL)**
> 
> SQL 是一种语言，用在大多数关系数据库的管理数据库中的数据。 该指南包含的命令，用于检索数据并更新它，并能够让你创建、 修改和管理数据库表。 SQL 是不同于编程语言 （如在 WebMatrix 中使用的一个） 因为 sql，思路是，您告诉数据库所需的并且它数据库的作业，以了解如何获取数据或执行任务。 下面是一些 SQL 命令的示例，以及他们执行的操作：
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 这会提取*Id*，*名称*，并*价格*中的记录中的列*产品*表如果的值*价格*大于 10，并将结果返回的值为基础的按字母顺序*名称*列。 此命令将返回包含满足条件或一个空集，如果没有与匹配记录的记录的结果集。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> 这会插入到一个新的记录*产品*表中，设置*名称*列&quot;新月形面包&quot;，则*说明*列&quot;不可靠兴致勃勃&quot;，和 1.99 的价格。
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 此命令删除中的记录*产品*其到期日期列是早于 2008 年 1 月 1 日的表。 (这假定*产品*表当然有这样的列。)此处采用 MM/DD/YYYY 格式输入日期，但它应在你的区域设置使用的格式输入。
> 
> `Insert Into`和`Delete`命令不返回结果集。 相反，它们返回一个数字，告知你多少条记录受影响的命令。
> 
> 对于某些操作 （如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。 这是用于生产数据库通常必须将连接到数据库时提供用户名和密码的原因。
> 
> 有许多 SQL 命令，但它们都遵循类似的模式。 SQL 命令可用于创建数据库表、 计算的表中的记录数、 计算价格，和执行很多更多操作。


## <a name="inserting-data-in-a-database"></a>在数据库中插入数据

本部分演示如何创建一个允许用户添加到新的产品页面*产品*数据库表。 插入新的产品记录后，页面将显示更新的表使用*ListProducts.cshtml*在上一节中创建的页。

此页包含验证以确保用户输入的数据是有效的数据库。 例如，在页中的代码可确保已为所有所需的列输入一个值。

1. 在网站中，创建一个名为的新的 CSHTML 文件*InsertProducts.cshtml*。
2. 使用以下内容替换现有标记：

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    页的正文包含一个 HTML 窗体使用户可以输入名称、 说明和价格的三个文本框。 当用户单击**插入**按钮，在页面顶部的代码打开的连接*SmallBakery.sdf*数据库。 然后获取在用户提交使用的值`Request`对象，并将这些值分配给本地变量。

    若要验证用户为每个所需的列输入一个值，则注册每个`<input>`你想要验证的元素：

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation`帮助程序会检查每个已注册的字段中不存在值。 你可以测试是否所有字段通过检查已都通过验证`Validation.IsValid()`，这通常执行之前处理从用户获取的信息：

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    (`&&`运算符表示 AND — 此测试是否*如果这是提交窗体和所有字段已都通过验证*。)

    如果验证了所有列 （不是空的），请继续并创建 SQL 语句插入数据并执行它按如下所示：

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    对于要插入的值，包括参数占位符 (`@0`， `@1`， `@2`)。

    > [!NOTE]
    > 作为安全预防措施，始终将值传递给 SQL 语句使用参数，如前面的示例中所示。 这使你可以验证用户的数据，以及它有助于防御恶意命令发送到数据库 （有时称为 SQL 注入式攻击） 的尝试。

    若要执行查询时，你使用此语句中，将其传递给包含要替换的占位符的值的变量：

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    之后`Insert Into`执行语句，将用户发送到页面，其中列出了使用下面这行的产品：

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    如果验证不成功，则跳过插入。 相反，可以显示累计的错误消息 （如果有） 的页面中有一个帮助程序：

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    请注意，在标记中的样式块包含 CSS 类定义名为`.validation-summary-errors`。 这是默认情况下使用的 CSS 类的名称`<div>`元素，其中包含任何验证错误。 在这种情况下，CSS 类指定验证摘要错误会显示为红色，并以粗体显示的但你可以定义`.validation-summary-errors`类，以显示您喜欢的格式设置。

### <a name="testing-the-insert-page"></a>测试插入页

1. 在浏览器中查看的页面。 该页将显示类似于下图中显示一个窗体。

    ![[image]](5-working-with-data/_static/image5.jpg)
2. 输入值的所有列，但请确保您离开*价格*列保留为空白。
3. 单击“插入” 。 页会显示错误消息，如下图中所示。 （不创建任何新记录。）

    ![[image]](5-working-with-data/_static/image6.jpg)
4. 完全，填写表单，然后依次**插入**。 这一次， *ListProducts.cshtml*页会显示，并显示新记录。

## <a name="updating-data-in-a-database"></a>更新数据库中的数据

数据进入一个表后，你可能需要更新它。 此过程演示如何创建类似于数据插入操作之前创建的两个页面。 第一页显示产品，并使用户可以选择另一个用于更改。 第二页允许用户实际上使所做的编辑，并将其保存。

> [!NOTE] 
> 
> **重要**在生产网站，您通常限制谁有权对数据进行更改。 有关如何设置成员资格以及方法可用来授予用户在站点上执行任务的信息，请参阅[添加安全性和 ASP.NET Web Pages 站点的成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。


1. 在网站中，创建一个名为的新的 CSHTML 文件*EditProducts.cshtml*。
2. 使用以下内容替换该文件中的现有标记：

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    此页之间唯一的区别并*ListProducts.cshtml*页上从前面是指在此页中的 HTML 表，包含显示的额外列**编辑**链接。 当单击此链接时，会转到*UpdateProducts.cshtml*页 （它将在下一步创建） 可以在其中编辑选定的记录。

    看一下创建的代码**编辑**链接：

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    这将创建对应的 HTML`<a>`元素的`href`动态设置属性。 `href`属性指定当用户单击该链接时要显示的页。 它还将`Id`到链接的当前行的值。 当运行页面时，页面源文件可能包含类似这样的链接：

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    请注意，`href`属性设置为`UpdateProducts/n`，其中*n*是产品编号。 当用户单击其中一个链接时，生成的 URL 将如下所示：

    `http://localhost:18816/UpdateProducts/6`

    换而言之，将在 URL 中传递的产品编号来对其进行编辑。
3. 在浏览器中查看的页面。 页面显示的数据的格式如下：

    ![[image]](5-working-with-data/_static/image7.jpg)

    接下来，您将创建可让用户实际更新的数据页。 更新页包括验证来验证用户输入的数据。 例如，在页中的代码可确保已为所有所需的列输入一个值。
4. 在网站中，创建一个名为的新的 CSHTML 文件*UpdateProducts.cshtml*。
5. 使用以下内容替换该文件中的现有标记。

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    页的正文包含 HTML 窗体，其中显示产品和用户可以在其中编辑。 若要获取产品以显示，您可以使用此 SQL 语句：

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    这将选择其 ID 与传入的值匹配的产品`@0`参数。 (因为*Id*是主键，因此必须是唯一的只能有一个产品记录可以不断选择这种方式。)若要获取的 ID 值要传递给此`Select`语句中，你可以读取的值传递到页 url，使用以下语法：

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    若要实际提取产品记录，应使用`QuerySingle`方法，它将返回一个记录：

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    到返回的单个行`row`变量。 可以从每个列获取数据并将其分配给本地变量如下：

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    在窗体的标记，这些值将显示自动在单个文本框中使用嵌入的代码如下所示：

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    该部分的代码显示更新的产品记录。 一旦已显示该记录，用户可以编辑各个列。

    当用户通过单击提交窗体**更新**按钮中的代码`if(IsPost)`块将运行。 这将获取用户的值从`Request`对象，将值存储在变量中，并验证每个列已填写。 如果通过了验证，代码会创建以下 SQL Update 语句：

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    在 SQL 中`Update`语句中，指定要将其设置为的值以及更新每个列。 在此代码中，这些值被指定使用参数占位符`@0`， `@1`， `@2`，依次类推。 （如前文所述，为了安全，您应始终将值传递给 SQL 语句使用的参数。）

    当您调用`db.Execute`方法，传递包含对应于 SQL 语句中的参数的顺序值的变量：

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    之后`Update`执行语句，以便将用户重定向回编辑页中调用以下方法：

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    其效果是用户将看到的已更新的列表的数据库中的数据，并可以编辑另一个产品。
6. 保存页。
7. 运行*EditProducts.cshtml*页面 （不是在更新页面），然后单击**编辑**来选择要编辑的产品。 *UpdateProducts.cshtml*显示页面时，显示所选的记录。

    ![[image]](5-working-with-data/_static/image8.jpg)
8. 进行更改，并单击**更新**。 具有更新数据再次显示产品列表。

## <a name="deleting-data-in-a-database"></a>删除数据库中的数据

本部分介绍如何让用户删除中的产品*产品*数据库表。 此示例由两个页面组成。 在第一页上，用户选择要删除的记录。 要删除的记录然后显示在第二个页中，让他们确认他们想要删除的记录。

> [!NOTE] 
> 
> **重要**在生产网站，您通常限制谁有权对数据进行更改。 有关如何设置成员资格以及方法可用来授予用户在站点上执行任务的信息，请参阅[添加安全性和 ASP.NET Web Pages 站点的成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。


1. 在网站中，创建一个名为的新的 CSHTML 文件*ListProductsForDelete.cshtml*。
2. 使用以下内容替换现有标记：

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    此页是类似于*EditProducts.cshtml*从前面的页。 但是，而不是显示**编辑**链接为每个产品，它将显示**删除**链接。 **删除**标记中使用下面的嵌入的代码创建链接：

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    这会创建如下所示，当用户单击该链接的 URL:

    `http://<server>/DeleteProduct/4`

    该 URL 调用一个名为页*DeleteProduct.cshtml* （这将在下一步创建） 并将其传递要删除的产品 ID （此处，4）。
3. 保存该文件，但使其保持打开状态。
4. 创建另一个名为的 CHTML 文件*DeleteProduct.cshtml*。 使用以下内容替换现有内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    调用此页面*ListProductsForDelete.cshtml*并使用户可以确认他们想要删除某个产品。 若要列出要删除的产品，您获取的产品 ID 从 URL 中删除使用以下代码：

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    页面然后会要求用户单击按钮，实际上删除的记录。 这是一种重要的安全措施： 时在你的网站等更新或删除数据中执行敏感操作，应始终执行这些操作使用 POST 操作，而不是 GET 操作。 如果你的站点设置，以便可以使用 GET 操作执行删除操作，任何人都可以传递的 URL，如`http://<server>/DeleteProduct/4`和从数据库中删除它们所需的所有操作。 通过添加确认并编写代码页，以便只能通过使用 POST 可以执行删除操作，向站点添加安全的措施。

    使用以下代码，首先确认这是 post 操作并且 ID 不为空可执行实际删除操作：

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    代码运行的 SQL 语句中删除指定的记录，然后将用户重定向回列表页。
5. 运行*ListProductsForDelete.cshtml*在浏览器中。

    ![[image]](5-working-with-data/_static/image9.jpg)
6. 单击**删除**链接的某个产品。 *DeleteProduct.cshtml*显示页以确认要删除该记录。
7. 单击**删除**按钮。 删除该产品记录，并使用更新的产品列表刷新页面。

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>连接到数据库
> 
> 您可以连接到两种方法中的数据库。 第一种是使用`Database.Open`方法，并指定数据库文件的名称 (更少 *.sdf*扩展):
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open`方法假设。*sdf*文件是在网站中*应用程序\_数据*文件夹。 此文件夹被专为保存数据。 例如，它具有相应权限以允许网站以读取和写入数据，并作为一种安全措施，WebMatrix 不允许访问文件从该文件夹。
> 
> 第二种方法是使用连接字符串。 连接字符串包含有关如何连接到数据库的信息。 这可能包括文件路径，也可能包括本地或远程服务器，以及用户名和密码以连接到该服务器上的 SQL Server 数据库的名称。 （如果您将数据保持集中管理版本的 SQL Server 中，如在托管提供商的网站上，你始终使用连接字符串来指定数据库连接信息。）
> 
> 在 WebMatrix 中，连接字符串通常存储在名为 XML 文件中*Web.config*。正如名称所示，可以使用*Web.config*你的网站以存储站点的配置信息，包括你的站点可能需要的任意连接字符串的根目录中的文件。 中的连接字符串的示例*Web.config*文件可能如下所示：
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 在示例中，连接字符串指向的数据库中的某处的服务器上运行的 SQL Server 实例 (而不是本地 *.sdf*文件)。 您需要替换为相应的名称`myServer`并`myDatabase`，并指定 SQL Server 登录名值`username`和`password`。 （用户名和密码值不一定相同作为 Windows 凭据或托管提供商提供你在登录到他们的服务器的值。 请与管理员联系的所需的确切值。）
> 
> `Database.Open`方法非常灵活，因为它允许您将数据库的名称传递 *.sdf*文件或存储在连接字符串的名称*Web.config*文件。 下面的示例演示如何连接到该数据库使用上一示例中所示的连接字符串：
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 如前所述，`Database.Open`方法允许您传递的数据库名称或连接字符串，并将找出要使用。 在部署时，这是非常有用 （发布） 你的网站。 可以使用 *.sdf*中的文件*应用\_数据*文件夹时在开发和测试你的站点。 然后，当将站点迁移到生产服务器时，可以使用中的连接字符串*Web.config*具有相同的名称的文件您 *.sdf*文件，但指向托管提供商的数据库&#8212;所有而无需更改代码。
> 
> 最后，如果你想要直接使用连接字符串，则可以调用`Database.OpenConnectionString`方法并传递它的实际连接字符串而不只需一个中的名称*Web.config*文件。 这可能很有用的情况下，由于某种原因不能访问的连接字符串 (或值，例如 *.sdf*文件名称) 之前的页面正在。 但是，大多数情况下，您可以使用`Database.Open`这篇文章中所述。


## <a name="additional-resources"></a>其他资源

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [连接到 SQL Server 或在 WebMatrix 中的 MySQL 数据库](https://go.microsoft.com/fwlink/?LinkId=208661)
- [在 ASP.NET 网站中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)
