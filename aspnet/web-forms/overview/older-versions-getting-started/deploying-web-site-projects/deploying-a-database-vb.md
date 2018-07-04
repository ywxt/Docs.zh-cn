---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
title: 部署数据库 (VB) |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET web 应用程序需要从开发环境中获取的必要的文件和资源到生产环境。 为 da...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/23/2009
ms.topic: article
ms.assetid: 96ac3e69-04c7-4917-ad06-5f8968c3fbf1
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 3dc5e9b4e189929b2b898b997b7577a623bdc8a7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381317"
---
<a name="deploying-a-database-vb"></a>部署数据库 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_VB.zip)或[下载 PDF](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_vb.pdf)

> 部署 ASP.NET web 应用程序需要从开发环境中获取的必要的文件和资源到生产环境。 对于数据驱动的 web 应用程序中，这包括数据库架构和数据。 本教程中探讨了成功部署到生产环境中开发环境的数据库所需的步骤一系列的第一个。


### <a name="introduction"></a>介绍

部署 ASP.NET web 应用程序需要从开发环境中获取的必要的文件和资源到生产环境。 在过去的过去六个教程还介绍了简单的书评 web 应用程序部署。 此演示站点已包含的服务器端资源的 ASP.NET 页、 配置文件中，许多`Web.sitemap`文件和等的以及客户端的资源，如图像和 CSS 文件。 但 web 应用程序的数据驱动的呢？ 必须采取哪些额外步骤来部署 web 应用程序使用数据库？

通过下一步的多个教程中，我们将解决部署数据驱动的 web 应用程序所需的步骤。 本教程首先会了解如何让数据库的架构和内容从开发环境到生产环境中，而后续的教程中探讨的所需的配置更改。 之后我们将探讨部署使用应用程序服务 （成员资格、 角色、 配置文件中，等） 的数据库的挑战。

## <a name="examining-the-updated-book-reviews-web-application"></a>检查更新的通讯簿评审 Web 应用程序

为了演示部署数据驱动的 web 应用程序，我已更新为数据驱动型从简单的静态网站书评 web 应用程序。 因为在这之前，有两个版本的此教程的下载中的应用程序： 一个使用 Web 应用程序项目模型，另一个使用网站项目模型。

更新的书评 web 应用程序使用[SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx)数据库，它存储在站点 s`App_Data`文件夹 (`~/App_Data/Reviews.mdf`)。 如果必须在计算机上安装 SQL Server 2008 然后演示将会正确运行。 如果有较旧版本的 SQL Server 可以安装免费的 SQL Server 2008 Express Edition，或者可以使用脚本可在本教程中 s 下载自行创建该数据库的数据库。

`Reviews.mdf`数据库包含四个表：

- `Genres` -包括每个流派，如技术、 小说和业务的记录。
- `Books` -包括每个评审，如列的记录`Title`， `GenreId`， `ReviewDate`，和`Review`，等等。
- `Authors` -包含有关已审阅书籍做出了贡献每位作者的信息。
- `BooksAuthors` -指定哪些作者已编写哪些丛书的多对多联接表。
  

图 1 显示了以下四个表的 ER 关系图。


[![通讯簿评审 Web 应用程序的数据库是包含的四个表](deploying-a-database-vb/_static/image2.jpg)](deploying-a-database-vb/_static/image1.jpg) 

**图 1**: 通讯簿评审 Web 应用程序的数据库是包含的四个表 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image3.jpg))


以前版本的书评网站必须单独每本书的 ASP.NET 页面。 例如，有了一个名为页`~/Tech/TYASP35.aspx`包含的审阅*教您自己 ASP.NET 3.5 24 小时内*。 该网站的此新数据驱动版本具有存储在数据库和单个 ASP.NET 页面，Review.aspx?ID= 评论*bookId*，后者将显示指定的书籍的审阅。 同样，没有 Genre.aspx?ID=*genreId*页面列出了指定的类型中的已审阅的书籍。

图 2 和 3 个 show`Genre.aspx`和`Review.aspx`操作中的页。 请注意每个页面在地址栏中的 URL。 在图 2 it s Genre.aspx？ ID = 85d164ba 1123年 4 c 的 47-82a0-c8ec75de7e0e。 因为 85d164ba-1123-4c47-82a0-c8ec75de7e0e`GenreId`技术 genre、"技术回顾"页的标题读取和项目符号列表的值枚举属于此类型在站点上的这些评论。


[![技术流派页](deploying-a-database-vb/_static/image5.jpg)](deploying-a-database-vb/_static/image4.jpg) 

**图 2**: 技术流派页 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image6.jpg))


[![有关查看自学 ASP.NET 3.5 中 24 小时](deploying-a-database-vb/_static/image8.jpg)](deploying-a-database-vb/_static/image7.jpg) 

**图 3**: 评审*教您自己 ASP.NET 3.5 24 小时内*([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image9.jpg))


通讯簿评审 web 应用程序还包括管理部分，管理员可以添加、 编辑和删除流派，评审，和作者信息。 目前，任何访问者可以访问管理部分。 在将来的教程中我们将添加对用户帐户的支持，并仅允许经过授权的用户到管理页。

如果您下载书评应用程序请记住，其目的是演示如何部署数据驱动的应用程序。 它不会出现就应用程序设计最佳实践。 例如，没有任何单独的数据访问层 (DAL);ASP.NET 页面直接与通过 SqlDataSource 控件或其代码隐藏类中的 ADO.NET 代码数据库进行通信。 有关创建数据驱动的应用程序使用分层体系结构的更深入信息，请参阅我[*使用的数据*教程](../../data-access/index.md)。

## <a name="databases-on-development-versus-production"></a>在开发与生产数据库

当您开始开发数据驱动的 web 应用程序时必须指定数据库连接字符串，提供有关如何连接到数据库的应用程序详细信息。 此连接字符串指定其他内容、 数据库服务器、 数据库名称和安全信息。 大多数情况下，应用程序在开发期间使用的数据库是不同于数据库时使用它在生产环境中的 s。 有很多好处的适用于开发与生产环境使用不同的数据库。 不要具有不同的数据库开发意味着您需要考虑如何意外修改或删除实时数据。 它还允许您将放入的虚拟测试数据或对数据模型进行重大更改，而无需担心如何在生产环境中应用程序的影响。 缺点不同的数据库开发和生产环境中是，当应用程序部署到数据库的架构数据库和相关的任何更改，或必须部署的数据。

在第一个部署前没有数据库，只有一个实例，该实例是在开发环境中。 部署到生产环境的第一次应用程序时我们不仅必须复制必要的服务器端和客户端的文件，而且还将开发环境中的数据库复制到生产环境。 这是在其中我们处在右，现在与书评 web 应用程序的数据库驻留在`App_Data`文件夹在我们的开发环境中但不是具有尚未被推送到生产环境。

一旦部署应用程序有两个数据库的副本。 随着应用程序日趋成熟，可能会添加新功能，因而需要进行数据模型的更改 （如将新列添加到现有表，对现有列，添加新表进行更改和其他操作）。 接下来的 web 应用程序部署，所做的更改应用于开发环境中的数据库中，由于上一个部署必须应用到生产数据库。 在将来的教程中讨论了一些策略可用于管理此过程。 本教程重点介绍部署到生产环境中开发环境的整个数据库。

## <a name="deploying-the-database-to-the-production-environment"></a>将数据库部署到生产环境

本教程的其余部分讨论如何部署到生产环境中开发环境的数据库。 如果您按照沿您需要确保您的帐户和 web 宿主提供程序包括 Microsoft SQL Server 数据库支持。 您还需要具有某些信息后，即数据库服务器名称、 数据库名称和用户名和密码用来连接到数据库。

在本教程前面所述，书评网站的数据库是存储在 SQL Server 2008 Express Edition 数据库`App_Data`文件夹。 它将一定会原因，部署此类数据库将十分简单，就像复制`App_Data`从开发环境到生产环境的文件夹。 但是，大多数 web 宿主提供程序不支持在托管数据库`App_Data`文件夹出于安全考虑。 相反，web 主机，其环境中的 SQL Server 数据库服务器上提供的帐户。 部署到生产环境中开发环境的数据库需要获取你在你的 web 主机的数据库服务器上注册的数据库。

那么，如何得知您的数据库开发环境中的生产环境？ 有几种方法来实现此目的具体取决于您的 web 主机提供服务。 可以使用某些主机，如 DiscountASP.NET，FTP 或可以根据实际的数据库的备份`.mdf`文件到你的网站，然后，从控制面板中，将备份文件还原或附加`.mdf`到 SQL Server 数据库服务器的文件。 使用此类工具将数据库部署非常简单，只复制`App_Data`到生产环境，然后将其附加通过控制面板的文件夹。 这可能是首次发布你的数据库的最简单且最快速方法。

另一种方法是使用数据库发布向导。 数据库发布向导为 Windows 桌面应用程序将生成的 SQL 命令以在其表中创建的表、 存储的过程、 视图、 用户定义的函数等-将数据库的架构和数据 （可选）。 你可以然后连接到 SQL Server Management Studio 通过在 web 主机提供程序的数据库服务器，然后执行此脚本以重复生产上的数据库。 更好，如果您的 web 主机提供商支持 Microsoft s [Database Publishing Services](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home)可以代表用户在数据库服务器上自动执行将数据库发布向导生成的脚本。 由于数据库发布向导生成创建的数据库的架构和数据的脚本，因此将工作而不考虑 web 主机提供商是否提供了功能，如附加已上传`.mdf`文件。

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>生成 SQL 命令来创建数据库架构和数据使用数据库发布向导

让我们来引导书评数据库部署到生产环境中使用数据库发布向导。 如果您使用的 Visual Studio 2008 或更高版本，已安装数据库发布向导。 如果您使用的 Visual Studio 2005，则您将需要先[下载并安装](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)向导。

打开 Visual Studio 并导航到`Reviews.mdf`数据库。 如果使用 Visual Web Developer 中，转到数据库资源管理器;如果使用的 Visual Studio，，使用服务器资源管理器。 图 4 显示了`Reviews.mdf`Visual Web Developer 中的数据库资源管理器中的数据库。 如图 4 所示，`Reviews.mdf`数据库组成的四个表、 三个存储的过程和用户定义函数。


[![在数据库资源管理器或服务器资源管理器中找到数据库](deploying-a-database-vb/_static/image11.jpg)](deploying-a-database-vb/_static/image10.jpg) 

**图 4**： 在数据库资源管理器或服务器资源管理器中找到数据库 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image12.jpg))


右键单击数据库名称，然后从上下文菜单中选择"发布到提供程序"选项。 这将启动数据库发布向导 （请参见图 5）。 单击旁边提前过去的初始屏幕。


[![数据库发布向导的初始屏幕](deploying-a-database-vb/_static/image14.jpg)](deploying-a-database-vb/_static/image13.jpg) 

**图 5**: 数据库发布向导初始屏幕 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image15.jpg))


在向导中的第二个屏幕列出了数据库发布向导可以访问数据库，并允许您选择是否要在所选数据库中的所有对象编写都脚本或选择编写都脚本的对象。 选择相应的数据库并将"对象所选数据库中的所有脚本"选项处于选中状态。

> [!NOTE]
> 如果收到错误"在数据库中有任何对象*databaseName*的此向导可编写脚本的类型"时在图 6 中所示的屏幕中单击下一步，请确保您的数据库文件的路径不是很长。 如中所述[这项讨论](http://www.codeplex.com/sqlhost/Thread/View.aspx?ThreadId=11014)在数据库发布向导项目页上，可能出现此错误，如果数据库文件的路径太长。


[![数据库发布向导的初始屏幕](deploying-a-database-vb/_static/image17.jpg)](deploying-a-database-vb/_static/image16.jpg) 

**图 6**: 数据库发布向导初始屏幕 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image18.jpg))


从下一个屏幕可以生成的脚本文件或者，如果你的 web 主机支持此功能，数据库将直接发布到 web 宿主提供程序的数据库服务器。 如图 7 所示，我遇到脚本写入到文件`C:\REVIEWS.MDF.sql`。


[![编写脚本的数据库的文件或将其发布到你的 Web 宿主提供程序直接](deploying-a-database-vb/_static/image20.jpg)](deploying-a-database-vb/_static/image19.jpg) 

**图 7**： 编写脚本的数据库的文件或将其发布到你的 Web 宿主提供程序直接 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image21.jpg))


后续屏幕将提示您输入的各种脚本编写选项。 您可以指定脚本是否应包含 drop 语句删除这些现有对象。 此值默认为 True，这样很好的第一次部署数据库时。 此外可以指定目标数据库是 SQL Server 2000、 SQL Server 2005 或 SQL Server 2008。 最后，指示是否编写脚本的架构和数据，只需的数据或只为架构。 架构是数据库对象、 表、 存储的过程、 视图和等等的集合。 数据是驻留在表中的信息。

如图 8 所示，我遇到配置为删除现有数据库对象，该向导生成脚本的 SQL Server 2008 数据库，并将发布架构和数据。


[![指定发布选项](deploying-a-database-vb/_static/image23.jpg)](deploying-a-database-vb/_static/image22.jpg) 

**图 8**： 指定的发布选项 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image24.jpg))


在最后两个屏幕总结了要执行，并显示的脚本状态的操作。 运行向导的最终结果是我们有一个包含生产上创建数据库并使用相同的数据填充它与在开发上所需的 SQL 命令的脚本文件。

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>在生产环境数据库上执行的 SQL 命令

现在，我们已经包含 SQL 命令来创建数据库和其数据保留的脚本是在生产数据库上执行该脚本。 某些 web 主机提供商提供其控制面板，您可以在其中输入要在数据库上执行的 SQL 命令中的文本框。 如果您有一个非常大的脚本文件，则此选项可能不起作用 (`REVIEWS.MDF.sql`脚本文件为超过 425 KB 的大小，例如)。

更好的方法是直接连接到生产数据库服务器使用 SQL Server Management Studio (SSMS)。 如果有非 Express Edition 的 SQL Server 计算机上安装然后可能已经安装 SSMS。 否则，你可以[下载并安装](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)SQL Server Management Studio Express Edition 的免费副本。

启动 SSMS 并连接到使用 web 主机提供商提供的信息在 web 主机的数据库服务器。


[![连接到 Web 宿主提供程序的数据库服务器](deploying-a-database-vb/_static/image26.jpg)](deploying-a-database-vb/_static/image25.jpg) 

**图 9**： 连接到你的 Web 主机提供商 s 数据库服务器 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image27.jpg))


展开数据库选项卡并找到你的数据库。 单击工具栏左上角中的新建查询按钮，将粘贴数据库发布向导中，创建的脚本文件中的 SQL 命令中，单击执行按钮以在生产数据库服务器上运行这些命令。 尤其是大型脚本文件时可能需要几分钟才能执行命令。


[![连接到 Web 宿主提供程序的数据库服务器](deploying-a-database-vb/_static/image29.jpg)](deploying-a-database-vb/_static/image28.jpg) 

**图 10**： 连接到你的 Web 主机提供商 s 数据库服务器 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image30.jpg))


该 s 都在这里就简单 ！ 现在，重复开发数据库到生产环境。 如果刷新该数据库在 SSMS 中的应看到新的数据库对象。 图 11 显示了生产数据库的表、 存储的过程和用户定义的函数，镜像上开发数据库。 和生产数据库的表我们指示数据库发布向导来将数据发布，因为具有在该向导已执行的时间与开发数据库的表相同的数据。 图 12 显示了中的数据`Books`生产数据库上的表。


[![在生产数据库上复制了数据库对象](deploying-a-database-vb/_static/image32.jpg)](deploying-a-database-vb/_static/image31.jpg) 

**图 11**: 数据库对象已复制了生产数据库上 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image33.jpg))


[![生产数据库包含与在开发数据库相同的数据](deploying-a-database-vb/_static/image35.jpg)](deploying-a-database-vb/_static/image34.jpg) 

**图 12**： 生产数据库上开发数据库包含相同的数据 ([单击以查看实际尺寸的图像](deploying-a-database-vb/_static/image36.jpg))


此时我们仅具有到生产环境部署开发数据库。 尚不支持已介绍了部署 web 应用程序本身或检查所需配置更改，让应用程序在生产使用生产数据库。 在下一教程中，我们将介绍这些问题 ！

## <a name="summary"></a>总结

部署数据驱动的 web 应用程序需要复制到生产环境的开发过程中使用的数据库。 许多 web 主机提供商提供工具来简化部署数据库的过程。 例如，使用 DiscountASP.NET 可以 FTP 数据库`.mdf`文件 （或备份），然后从控制面板将数据库附加到数据库服务器。 无论何种功能正常运行的另一个选项 web 主机提供商产品/服务是 Microsoft 的数据库发布向导工具，它会生成一个脚本用于创建开发数据库的架构和数据的 SQL 命令。 生成此脚本后您可以在生产数据库上执行它。

现在，书评 web 应用程序的数据库是生产上我们可以将部署应用程序。 但是，web 应用程序的配置信息指定到的数据库的连接字符串，该连接字符串引用开发数据库。 我们需要更新此连接字符串信息时在将站点部署到生产环境。 下一教程探讨这些配置差异，并逐步介绍数据驱动的书评站点发布到生产环境所需的步骤。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [下载 Microsoft SQL Server 数据库发布向导 1.1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [下载 Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [上一页](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
> [下一页](configuring-the-production-web-application-to-use-the-production-database-vb.md)
