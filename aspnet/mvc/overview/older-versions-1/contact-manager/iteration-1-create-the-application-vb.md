---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 迭代 1 – 创建应用程序 (VB) |Microsoft Docs
author: microsoft
description: 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和 D....
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: aee177164293c178fa7d2d4acfb60f85dc98bb05
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802998"
---
<a name="iteration-1--create-the-application-vb"></a>迭代 1 – 创建应用程序 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1-创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3-添加窗体验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4-使应用程序松散耦合。 在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6-使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7-添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。

## <a name="this-iteration"></a>此迭代

在此第一个迭代中，我们构建的基本应用程序。 目标是尽可能最快且最简单方式构建联系人管理器。 在更高版本迭代中，我们改进应用程序的设计。

联系人管理器应用程序是一个基本的数据库驱动的应用程序。 应用程序可用于创建新的联系人、 编辑现有联系人和删除联系人。

在此迭代中，我们将完成以下步骤：

1. ASP.NET MVC 应用程序
2. 创建一个数据库来存储我们的联系人
3. 生成模型类，以便使用我们的 Microsoft 实体框架的数据库
4. 创建控制器操作和视图，使我们能够列出所有数据库中的联系人
5. 创建控制器操作和视图，使我们能够在数据库中创建一个新的联系人
6. 创建控制器操作和使我们能够编辑现有联系人数据库中的视图
7. 创建控制器操作和使我们能够删除现有数据库中的联系人的视图

## <a name="software-prerequisites"></a>软件必备项

在 ASP.NET MVC 应用程序中，您必须具有 Visual Studio 2008 或 （Visual Web Developer 不包含所有 Visual Studio 的高级功能的 Visual Studio 的免费版本) 在计算机上安装 Visual Web Developer 2008。 可以从以下地址下载是 Visual Studio 2008 试用版或 Visual Web Developer:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 使用 Visual Web Developer 的 ASP.NET MVC 应用程序，您必须安装的 Visual Web Developer Service Pack 1。 不带 Service Pack 1，无法创建 Web 应用程序项目。


ASP.NET MVC 框架。 您可以从以下地址下载 ASP.NET MVC framework:

[https://www.asp.net/mvc](../../../index.md)

在本教程中，我们可以使用 Microsoft Entity Framework 访问数据库。 实体框架将附带.NET Framework 3.5 Service Pack 1。 可以从以下位置下载此 service pack:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&ampdisplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

为执行每个这些下载的替代方法，可以充分利用 Web 平台安装程序 (Web PI)。 您可以从以下地址下载 Web PI:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 项目

ASP.NET MVC Web 应用程序项目。 启动 Visual Studio 并选择菜单选项**文件，新的项目**。 **新的项目**对话框 （请参见图 1）。 选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。 为新项目命名*ContactManager* ，然后单击确定按钮。


请确保你具有从顶部的下拉列表中选择的.NET Framework 3.5 角**新的项目**对话框。 否则，赢得 t 的 ASP.NET MVC Web 应用程序模板显示。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**图 01**: 新建项目对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image2.png))


ASP.NET MVC 应用程序**创建单元测试项目**此时将显示对话框。 可以使用此对话框以指示你想要创建并创建 ASP.NET MVC 应用程序时向你的解决方案添加单元测试项目。 尽管我们获得了 t 是构建此小版本中的单元测试，应选择选项**可以，请创建单元测试项目**由于我们计划在后续迭代中添加单元测试。 首次创建新的 ASP.NET MVC 项目时添加的测试项目是比创建 ASP.NET MVC 项目后再添加一个测试项目容易得多。

> [!NOTE] 
> 
> Visual Web Developer 不支持测试项目，因为您无法获得创建单元测试项目对话框中，当使用 Visual Web Developer。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**图 02**: 创建单元测试项目对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image4.png))


ASP.NET MVC 应用程序将显示在 Visual Studio 解决方案资源管理器窗口 （请参见图 3）。 如果 don t 看到解决方案资源管理器窗口，然后通过选择菜单选项可打开此窗口**视图、 解决方案资源管理器**。 请注意，该解决方案包含两个项目： 在 ASP.NET MVC 项目和测试项目。 ASP.NET MVC 项目命名为 ContactManager 和测试项目命名为 ContactManager.Tests。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**图 03**: 解决方案资源管理器窗口 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image6.png))


## <a name="deleting-the-project-sample-files"></a>删除项目示例文件

ASP.NET MVC 项目模板包括用于控制器和视图的示例文件。 在创建新的 ASP.NET MVC 应用程序之前, 应删除这些文件。 您可以删除文件和文件夹在解决方案资源管理器窗口中的右键单击文件或文件夹并选择菜单选项**删除**。

需要从 ASP.NET MVC 项目中删除以下文件：

- \Controllers\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

并且，需要从测试项目中删除以下文件：

\Controllers\HomeControllerTest.vb

## <a name="creating-the-database"></a>创建数据库

联系人管理器应用程序是一个数据库驱动的 web 应用程序。 我们使用数据库来存储联系人信息。

使用包括 Microsoft SQL Server、 Oracle、 MySQL 和 IBM DB2 数据库的任何现代数据库在 ASP.NET MVC framework。 在本教程中，我们使用 Microsoft SQL Server 数据库。 在安装 Visual Studio，则会安装 Microsoft SQL Server Express 是免费版本的 Microsoft SQL Server 数据库的选项。

通过右键单击该应用程序创建新的数据库\_在解决方案资源管理器窗口并选择菜单选项中的数据文件夹**添加、 新项**。 在中**添加新项**对话框中，选择**数据**类别并**SQL Server 数据库**模板 （请参阅图 4）。 命名新数据库 ContactManagerDB.mdf，然后单击确定按钮。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**图 04**： 创建新的 Microsoft SQL Server Express 数据库 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image8.png))


创建新的数据库后，数据库会显示在应用中\_在解决方案资源管理器窗口中的数据文件夹。 双击 ContactManager.mdf 文件以打开服务器资源管理器窗口并连接到数据库。

> [!NOTE] 
> 
> 服务器资源管理器窗口调用在 Microsoft Visual Web Developer 的情况下的数据库资源管理器窗口。


服务器资源管理器窗口可用于创建新的数据库对象，如数据库表、 视图、 触发器和存储的过程。 右键单击表文件夹，然后选择菜单选项**添加新表**。 数据库表设计器将显示 （请参见图 5）。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**图 05**： 数据库表设计器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image10.png))


我们需要创建一个表格，包含以下列：

<a id="0.2_table01"></a>


| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | int | False |
| FirstName | nvarchar （50) | False |
| LastName | nvarchar （50) | False |
| 电话 | nvarchar （50) | False |
| 电子邮件 | nvarchar(255) | False |


第一列，Id 列中，比较特殊。 您需要将 Id 列标记为标识列和主键列。 您指示某一列为标识列展开列属性 （请查看底部的图 6），然后滚动到标识规范属性。 设置 **（是标识）** 属性设置为值**是**。

通过选择列并单击带有密钥的图标的按钮可将列标记为 Primary Key 列中。 某列标记为 Primary Key 列后，列的旁边会显示密钥的一个图标 （请参阅图 6）。

完成创建表后，单击保存按钮 （带有软盘图标的按钮） 以保存新表。 将新表命名*联系人*。

之后创建的联系人数据库表的完成，应将某些记录添加到表中。 右键单击服务器资源管理器窗口中的联系人表，然后选择菜单选项**显示表数据**。 将显示为网格中输入一个或多个联系人。

## <a name="creating-the-data-model"></a>创建数据模型

ASP.NET MVC 应用程序包含的模型、 视图和控制器。 我们首先创建一个表示联系人表，我们在上一节中创建的模型类。

在本教程中，我们可以使用 Microsoft Entity Framework 自动从数据库生成模型类。

> [!NOTE] 
> 
> ASP.NET MVC 框架不依赖于 Microsoft Entity Framework 以任何方式。 可以使用备用数据库访问技术，包括 NHibernate、 LINQ to SQL 或 ADO.NET 使用 ASP.NET MVC。


请执行以下步骤来创建数据模型类：

1. 右键单击解决方案资源管理器窗口中的 Models 文件夹，然后选择**添加、 新项**。 **添加新项**对话框 （请参见图 6）。
2. 选择**数据**类别和**ADO.NET 实体数据模型**模板。 命名你的数据模型*ContactManagerModel.edmx*然后单击**添加**按钮。 实体数据模型向导将显示 （请参阅图 7）。
3. 在中**选择模型内容**步骤中，选择**从数据库生成**（请参阅图 7）。
4. 在中**选择数据连接**步骤，选择 ContactManagerDB.mdf 数据库并输入名称*ContactManagerDBEntities* （请参阅图 8） 的实体连接设置。
5. 在中**选择数据库对象**步骤中，选择标记为的表 （请参阅图 9） 复选框。 数据模型将包括包含 （仅一个联系人表没有） 在数据库中的所有表。 输入的命名空间*模型*。 单击完成按钮以完成向导。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**图 06**: 添加新项对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image12.png))


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**图 07**： 选择模型内容 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image14.png))


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**图 08**： 选择数据连接 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image16.png))


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**图 09**： 选择数据库对象 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image18.png))


完成实体数据模型向导后，将显示实体数据模型设计器。 在设计器为要建模的每个表显示相对应的类。 应会看到一个名为联系人的类。

实体数据模型向导将生成基于数据库表名称的类名称。 几乎总是需要更改由向导生成的类的名称。 右键单击设计器中的联系人类，然后选择菜单选项**重命名**。 将类的名称从联系人 （复数） 更改为联系人 （单数形式）。 更改类名称后，此类应类似于图 10。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**图 10**: Contact 类 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image20.png))


此时，我们创建了我们的数据库模型。 我们可以使用联系人类来表示数据库中的特定联系人记录。

## <a name="creating-the-home-controller"></a>创建主控制器

下一步是创建我们的主控制器。 主控制器是 ASP.NET MVC 应用程序中调用的默认控制器。

通过右键单击解决方案资源管理器窗口中的 Controllers 文件夹并选择菜单选项创建主页控制器类**添加、 控制器**（请参阅图 11）。 请注意，标记为复选框**添加用于创建、 更新和的详细信息方案的操作方法**。 请确保单击前确认已选中此复选框**添加**按钮。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**图 11**： 添加主控制器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image22.png))


创建主控制器时，您在列表 1 中获取类。

**代码清单 1-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>列出联系人

若要显示的联系人数据库表中的记录，我们需要创建 index （） 操作和索引视图。

主控制器已包含 index （） 操作。 我们需要修改此方法，使它看起来像列表 2。

**代码清单 2-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

请注意，代码清单 2 中的主页控制器类包含一个名为的私有字段\_实体。 \_实体字段表示的实体数据模型中。 我们使用\_实体字段以与数据库通信。

Index （） 方法返回表示所有联系人联系人数据库表中的视图。 表达式\_实体。ContactSet.ToList() 泛型列表的形式返回联系人的列表。

现在，我们制作了索引控制器中，我们接下来需要创建索引视图。 在创建索引视图之前, 编译应用程序通过选择菜单选项**生成，生成解决方案**。 始终应添加一个视图，以便模型类的列表中显示之前编译你的项目**添加视图**对话框。

右键单击 index （） 方法并选择菜单选项创建索引视图**添加视图**（请参阅图 12）。 选择此菜单选项将打开**添加视图**对话框 （请参阅图 13）。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**图 12**： 添加索引视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image24.png))


在中**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。 选择视图数据类 ContactManager.Contact 和查看内容列表。 选择以下选项将生成一个视图，显示联系人记录的列表。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**图 13**: 添加视图对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image26.png))


当您单击**添加**生成按钮，清单 3 中的索引视图。 请注意&lt;%@ 页 %&gt;文件的顶部显示的指令。 索引视图继承自 ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt;类。 换而言之，在视图模型类表示联系人实体的列表。

索引视图，正文将包含 foreach 循环循环访问每个 Model 类所表示的联系人。 Contact 类的每个属性的值显示在 HTML 表。

**代码清单 3-Views\Home\Index.aspx （未修改）**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

我们需要使索引视图到一处修改。 因为我们不创建详细信息视图，我们可以删除的详细信息链接。 找到并从索引视图中删除以下代码：

{.id = 项。Id}) %&gt;

修改索引视图后，可以运行联系人管理器应用程序。 选择启动调试菜单选项调试，或只需按 F5。 首次运行该应用程序，您会得到对话框图 14 中。 选择的选项**修改 Web.config 文件以启用调试**，然后单击确定按钮。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**图 14**： 启用调试 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image28.png))


默认情况下返回索引视图。 此视图将列出所有联系人数据库表中的数据 （请参阅图 15）。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**图 15**： 该索引视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image30.png))


请注意，索引视图包含将标记为新创建的视图的底部的链接。 在下一步部分中，您将了解如何创建新的联系人。

## <a name="creating-new-contacts"></a>创建新的联系人

若要使用户能够创建新的联系人，我们需要将两个 create （） 操作添加到 Home 控制器。 我们需要创建一个返回 HTML 窗体创建一个新的联系人的 create （） 操作。 我们需要创建一个执行实际的数据库插入的新联系人的第二个 create （） 操作。

列表 4 中包含我们需要将添加到 Home 控制器的新 create （） 方法。

**列表 4-Controllers\HomeController.vb （与创建的方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

可以仅由 HTTP POST 调用的第二个 create （） 方法时，可以使用 HTTP GET 调用的第一个 create （） 方法。 换而言之，仅当发布 HTML 窗体时，可以调用第二个 create （） 方法。 第一个 create （） 方法只是返回一个包含用于创建新的联系人的 HTML 窗体视图。 第二个 create （） 方法是更有意义： 它向数据库添加新联系人。

请注意，第二个 create （） 方法已被修改以接受 Contact 类的实例。 发布从 HTML 窗体的窗体值绑定到此 Contact 类的是 ASP.NET MVC 框架自动。 创建 HTML 窗体中的每个窗体字段分配给联系人参数的属性。

请注意，使用 [Bind] 属性修饰联系人参数。 [Bind] 属性用于从绑定中排除的联系人 Id 属性。 由于 Id 属性表示的标识属性，我们不想要设置的 Id 属性。

在 create （） 方法的正文中，实体框架用于数据库中插入新的联系人。 新联系人添加到联系人的现有设置并调用 savechanges （） 方法来将这些更改推送回基础数据库。

您可以生成用于创建新的联系人，右键单击任意一种两个 create （） 方法并选择菜单选项的 HTML 窗体**添加视图**（请参阅图 16）。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**图 16**： 添加创建视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image32.png))


在中**添加视图**对话框中，选择**ContactManager.Contact**类并**创建**视图内容的选项 （请参阅图 17）。 当您单击**添加**按钮的创建自动生成视图。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**图 17**： 看到 explode 页面 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image34.png))


创建视图包含的 Contact 类属性的每个窗体字段。 列表 5 中包含创建视图的代码。

**列表 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

修改 create （） 方法并添加创建视图后，可以运行联系人管理器应用程序，并创建新的联系人。 单击**创建新**要导航到创建视图的索引视图中显示链接。 应会看到图 18 中的视图。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**图 18**: 创建视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image36.png))


## <a name="editing-contacts"></a>编辑联系人

添加编辑联系人记录的功能是非常类似于添加用于创建新联系人记录功能。 首先，我们需要将两个新的编辑方法添加到 Home 控制器类。 列表 6 中包含这些新的 edit （） 方法。

**代码清单 6-Controllers\HomeController.vb （与编辑方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

第一种 edit （） 方法调用的 HTTP GET 操作。 Id 参数传递给此方法，它表示正在编辑的联系人记录 Id。 实体框架用于检索与 id 匹配的联系人返回一个包含 HTML 窗体以编辑记录视图。

第二个 edit （） 方法来执行实际更新到数据库。 此方法作为参数接受 Contact 类的实例。 ASP.NET MVC 框架将绑定窗体字段中编辑窗体到此类自动。 编辑的联系人 （我们需要 Id 属性的值） 时，请注意，您不 t 包括 [Bind] 属性。

实体框架用于将已修改的联系人保存到数据库。 必须首先从数据库检索原始联系人。 接下来，调用 Entity Framework ApplyPropertyChanges() 方法来记录对联系人的更改。 最后，调用 Entity Framework savechanges （） 方法来保留对基础数据库的更改。

你可以生成包含右键单击 edit （） 方法并选择添加视图菜单选项编辑窗体的视图。 在添加视图对话框中，选择**ContactManager.Models.Contact**类和**编辑**查看内容 （请参阅图 19）。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**图 19**： 添加一个编辑视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image38.png))


当你单击添加按钮时，将自动生成新的编辑视图。 生成的 HTML 窗体包含对应于每个联系人类 （请参阅列表 7） 的属性的字段。

**列表 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>删除联系人

如果你想要删除的联系人，则需要将两个 delete （） 操作添加到 Home 控制器类。 第一个 delete （） 操作显示一个删除确认窗体。 第二个 delete （） 操作执行实际删除。

> [!NOTE] 
> 
> 更高版本，在迭代 #7 中，我们修改联系人管理器，以便它支持 Ajax 删除一个步骤。


代码清单 8 中包含两个新 delete （） 方法。

**代码清单 8-Controllers\HomeController.vb （删除方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

第一个 delete （） 方法返回用于从数据库中删除联系人记录的确认窗体 （请参阅 Figure20）。 第二个 delete （） 方法执行实际删除操作针对的数据库。 从数据库中检索原始联系人后，调用的实体框架 DeleteObject() 和 savechanges （） 方法来执行数据库删除。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**图 20**： 删除确认视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image40.png))


我们需要修改索引视图，使其包含用于删除联系人记录 （请参阅图 21） 的链接。 需要将以下代码添加到同一个表包含的单元格的编辑链接：

{.id = 项。Id}) %&gt;


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**图 21**： 索引视图与编辑链接 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image42.png))


接下来，我们需要创建删除确认视图。 右键单击主页控制器类中的 delete （） 方法并选择添加视图菜单选项。 添加视图对话框中显示 （请参阅图 22）。

与不同的列表、 创建和编辑视图中，在添加视图对话框中不包含创建删除视图的选项。 相反，选择**ContactManager.Models.Contact**数据类和**空**查看内容。 选择空视图内容的选项都需要我们自己创建的视图。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**图 22**： 添加删除确认视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image44.png))


删除视图的内容包含在程序列表 9。 此视图包含确认的窗体应为特定联系人是否删除 （请参阅图 21）。

**列表 9-Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>更改默认控制器的名称

它可能会给您带来麻烦的我们的控制器类名称使用联系人名为 HomeController 类。 长度应不 t 将控制器命名为 ContactController？

此问题很容易修复。 首先，我们需要重构的主控制器的名称。 Visual Studio 代码编辑器中打开 HomeController 类中，右键单击类的名称并选择菜单选项**重命名**。 选择此菜单选项打开重命名对话框。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**图 23**： 重构控制器名称 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image46.png))


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**图 24**： 使用重命名对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image48.png))


如果您重命名控制器类，Visual Studio 将更新视图文件夹中的文件夹的名称。 Visual Studio 将重命名为 \Views\Contact 文件夹 \Views\Home 文件夹。

进行此更改后，你的应用程序将不再具有主控制器。 运行你的应用程序时，会图 25 中显示错误页。


[![新建项目对话框](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**图 25**： 没有默认控制器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image50.png))


我们需要更新使用而不是主控制器的联系控制器在 Global.asax 文件中的默认路由。 打开 Global.asax 文件并修改默认控制器使用的默认路由 （请参阅代码清单 10）。

**代码清单 10-Global.asax.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

进行这些更改后，联系人管理器将正常运行。 现在，它将用作默认控制器 Contact 控制器类。

## <a name="summary"></a>总结

在此第一次迭代中，我们创建一个基本的联系人管理器应用程序中的最快方法可能。 我们可利用 Visual Studio 自动生成有关我们的控制器和视图的初始代码了。 我们还利用了实体框架可以自动生成我们的数据库模型类。

目前，我们可以列出、 创建、 编辑和删除联系人与联系人管理器应用程序记录。 换而言之，我们可以执行所有数据库驱动的 web 应用程序所需的基本数据库操作。

遗憾的是，我们的应用程序有一些问题。 第一，我不愿意再不得不承认，联系人管理器应用程序不是最具吸引力的应用程序。 它需要一些设计工作。 在下一个迭代中，我们将介绍如何更改默认视图母版页和级联样式表，以改善应用程序的外观。

其次，我们尚未实现任何窗体验证。 例如，没有执行任何操作，以防用户提交创建联系人窗体而无需任何窗体字段输入值。 此外，可以输入无效的电话号码和电子邮件地址。 我们首先来解决这个问题在迭代 #3 中的窗体验证。

最后，并最重要的是，联系人管理器应用程序的当前迭代无法轻松地修改或维护。 例如，数据库访问逻辑的控制器操作中已包含右。 这意味着，我们不能修改数据访问代码，而无需修改我们的控制器。 在后续迭代中，我们将探讨我们可以实现以使联系人管理器更具弹性，若要更改的软件设计模式。

> [!div class="step-by-step"]
> [上一页](iteration-7-add-ajax-functionality-cs.md)
> [下一页](iteration-2-make-the-application-look-nice-vb.md)
