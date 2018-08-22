---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
title: 配置生产 Web 应用程序以使用生产数据库 (VB) |Microsoft Docs
author: rick-anderson
description: 如之前教程中所述，它不是常见的配置信息以在开发和生产环境之间存在差异。 这是 es...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: a64a7aa0-6608-449e-83bf-1ef8cceee504
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 3d6e25de44a7c84ef0919d1cfd8ab4c6b368e0ea
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824886"
---
<a name="configuring-the-production-web-application-to-use-the-production-database-vb"></a>配置生产 Web 应用程序以使用生产数据库 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_VB.zip)或[下载 PDF](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_vb.pdf)

> 如之前教程中所述，它不是常见的配置信息以在开发和生产环境之间存在差异。 因为数据库连接字符串的开发和生产环境之间存在差异，这是对于数据驱动的 web 应用程序，尤其如此。 本教程探讨了如何配置在生产环境中更多详细信息包括适当的连接字符串。


## <a name="introduction"></a>介绍

数据驱动的 web 应用程序通常在生产环境中使用不同的数据库时比开发中。 对于应用程序由 web 主机提供商托管和本地开发，开发数据库通常驻留在开发人员的计算机上的生产数据库托管在 web 托管公司的设施的数据库服务器上时。 部署数据驱动的 web 应用程序时，需要将开发数据库复制到生产数据库服务器。 上一教程中我们介绍了如何完成此步骤。

Web 应用程序使用中的信息*连接字符串*建立与数据库的连接。 连接字符串，通常存储在`Web.config`，指定数据库服务器名称、 数据库、 安全上下文中和其他信息的名称。 因为 web 应用程序使用的数据库依赖于是否在开发或生产环境中运行 web 应用程序，连接字符串必须在两种环境之间有所不同。

不常见的配置信息以在开发和生产环境之间存在差异。 *常见配置差异之间开发和生产*教程讨论了用于上维护单独的配置之间这两种环境以及简要介绍的信息的方法数据库连接字符串。 本教程探讨了如何配置在生产环境中更多详细信息包括适当的连接字符串。

## <a name="examining-the-connection-string-information"></a>检查连接字符串信息

书评 web 应用程序使用的连接字符串存储在应用程序的配置文件， `Web.config`。 `Web.config` 包括用于存储连接字符串，正如其名为某个特殊部分[ &lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)。 `Web.config`书评网站有一个名为本部分中定义的连接字符串文件`ReviewsConnectionString`:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample1.xml)]

连接字符串的数据源 =。 \SQLEXPRESS;AttachDbFilename = |DataDirectory|\Reviews.mdf;Integrated Security = True;用户实例 = True-是组成大量的选项和值，使用选项/值对由分号和每个选项分隔和由等号分隔的值。 此连接字符串中使用的四个选项是：

- `Data Source` -指定数据库服务器和数据库服务器实例名称的位置 （如果有）。 值， `.\SQLEXPRESS`，是一个示例的数据库服务器和实例名称。 周期指定数据库服务器是作为该应用程序; 在同一计算机上实例名称是`SQLEXPRESS`。
- `AttachDbFilename` -指定数据库文件的位置。 值包含占位符`|DataDirectory|`，这是解析为 s 的应用程序的完整路径`App_Data`在运行时文件夹。
- `Integrated Security` -一个布尔值，该值指示是否使用指定的用户名/密码连接到数据库 (false) 或当前的 Windows 帐户凭据 (true) 时。
- `User Instance` -特定于 SQL Server Express 版本，该值指示是否允许在本地计算机上的非管理用户附加并连接到 SQL Server Express Edition 数据库的配置选项。 请参阅[SQL Server Express 用户实例](https://msdn.microsoft.com/library/ms254504.aspx)有关此设置的详细信息。
  

允许的连接字符串选项取决于要连接到数据库并[ADO.NET](http://ADO.NET)所使用的数据库提供程序。 例如，用于连接到 Microsoft SQL Server 数据库具有不同的用来连接到 Oracle 数据库连接字符串。 同样，连接到使用 SqlClient 提供程序的 Microsoft SQL Server 数据库使用不同的连接字符串比时使用的 OLE DB 访问接口。

可以通过使用之类的站点的手动生成的数据库连接字符串[ConnectionStrings.com](http://www.connectionstrings.com/)为哪些选项是可用的资源。 但是，较简单的方法是将数据库添加到 Visual Studio 中的服务器资源管理器，然后获取属性窗口中的连接字符串。 让我们来使用后一技术用于构造生产数据库服务器的连接字符串。

打开 Visual Studio，然后导航到服务器资源管理器窗口 （在 Visual Web Developer 中，此窗口被称为数据库资源管理器）。 右键单击数据连接选项，然后从上下文菜单中选择添加连接选项。 此时将显示在图 1 中所示的向导。 选择适当的数据源并单击继续。


[![选择将新的数据库添加到服务器资源管理器](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image1.jpg) 

**图 1**： 选择将新的数据库添加到服务器资源管理器 ([单击以查看实际尺寸的图像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image3.jpg))


接下来，指定的各种数据库连接信息 （请参见图 2）。 当您使用您的 web 托管公司注册它们应如何连接到数据库的数据库服务器名称、 数据库名称、 用户名和密码用于连接到数据库，依次类推提供了信息。 输入此信息后，单击确定以完成此向导并将数据库添加到服务器资源管理器。


[![指定的数据库连接信息](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image4.jpg) 

**图 2**： 指定数据库连接信息 ([单击以查看实际尺寸的图像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image6.jpg))


生产环境数据库现在应在服务器资源管理器中列出。 从服务器资源管理器中选择数据库并转到属性窗口。 可以在其中找到一个名为使用数据库 s 的连接字符串的连接字符串属性。 假设在生产和 SqlClient 提供程序上使用的 Microsoft SQL Server 数据库连接字符串应类似于下面：

<strong>数据源 =<em>serverName</em>;初始目录 =<em>databaseName</em>;持久性安全信息 = True;用户 ID =<em>用户名</em>;密码 =*密码</strong>*

其中*serverName*， *databaseName*，*用户名*，以及*密码*都替换为数据库服务器名称，该数据库的值名称，以及用户名和密码提供给你的 web 主机公司。

## <a name="deploying-the-book-reviews-web-application"></a>通讯簿评审 Web 应用程序部署

前面的教程分步说明了将开发数据库复制到生产环境中，但无法浏览部署数据驱动应用程序。 此时在生产环境包含的数据库，但正在使用静态评审使用通讯簿评审应用程序的版本。 我们需要新的数据驱动应用程序部署到生产服务器以及更新的配置信息。

请花费片刻时间部署数据驱动应用程序从开发环境到生产环境。 此过程已在前面的教程中详细介绍。 如果你需要复习，请参阅*部署在网站中使用 FTP 客户端*或*部署您的网站使用的 Visual Studio*教程。 您将需要确保生产数据库连接字符串是一个用于生产环境，这意味着备用`Web.config`文件必须部署。 具体而言，此修改`Web.config`文件的`<connectionStrings>`元素需要包含生产数据库连接字符串且应类似于以下：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample2.xml)]

请注意，该连接字符串中`<connectionStrings>`元素的名称 (`ReviewsConnectionString`)，但现在包含生产数据库连接字符串而不是开发数据库连接字符串。

除非有更正式的部署工作流，请手动修改`Web.config`文件部署 （请记住要恢复为使用开发的数据库连接字符串之前使用生产数据库连接字符串之后） 或维护一个单独`Web.config`获取作为部署过程的一部分上载到生产环境的生产环境配置信息的文件。

> [!NOTE]
> 如果意外地部署`Web.config`包含开发数据库连接字符串，则当对生产应用程序尝试连接到数据库将处于错误的文件。 此错误表现为`SqlException`reporting 服务器找不到或无法访问的消息。


在站点部署到生产环境后，请访问生产站点，通过浏览器。 应查看，并在本地运行数据驱动的应用程序时享受相同的用户体验。 当然生产上访问该网站时该站点由提供支持，生产数据库服务器上，而在开发过程中访问网站开发环境中的使用的数据库。 图 3 显示了*教您自己 ASP.NET 3.5 24 小时内*查看页上从生产环境 （请注意浏览器的地址栏中的 URL） 中的网站。


[![数据驱动应用程序已在现在可在生产环境 ！](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image7.jpg) 

**图 3**: The Data-Driven 应用程序已在现在可在生产环境 ！ ([单击此项可查看原尺寸图像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image9.jpg))


### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>将连接字符串存储在单独的配置文件

维护开发和生产环境的单独的配置信息的常用技术是具有两个版本的`Web.config`： 一个用于开发环境，另一个用于生产。 在部署时相应`Web.config`版本可以复制到生产环境。 理想情况下，将作为部署工作流的一部分自动执行此过程。

而不是维护两个单独`Web.config`文件 （可选） 可以提供更精细的差异。 元素构成`Web.config`然后在中引用的外部配置文件中，可以定义文件`Web.config`文件。 在简单地说有一个`Web.config`文件引用 databaseConnectionStrings.config 文件，将包含连接字符串这两个环境使用的应用程序，并且将是唯一的每个环境。 找到分离到单独的文件的不同配置信息提供整洁且更简单`Web.config`文件和详细清晰地概述了开发和生产环境之间的配置差异。

若要使用此方法，开始通过在名为 web 应用程序中创建一个新文件夹`ConfigSections`。 接下来，将两个文件添加到名为 databaseConnectionStrings.dev.config 和 databaseConnectionStrings.production.config 此新文件夹。接下来，复制`<connectionStrings>`元素从`Web.config`databaseConnectionStrings.dev.config 和 databaseConnectionStrings.production.config 文件，然后修改中的连接字符串databaseConnectionStrings.production.config 文件，以便指定要生产数据库连接字符串。 例如，databaseConnectionStrings.dev.config 文件应包含只`<connectionStrings>`引用开发数据库的连接字符串的元素：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample3.xml)]

同样，databaseConnectionStrings.production.config 文件应只包含`<connectionStrings>`元素，但具有生产数据库连接字符串。

制作一份 databaseConnectionStrings.dev.config 文件并将其命名 databaseConnectionStrings.config。

> [!NOTE]
> 您可以将配置文件名称以外的 databaseConnectionStrings.config，如 d，如`connectionStrings.config`或`dbInfo.config`。 但是，请确保使用该文件命名`.config`扩展插件作为`.config`文件，默认情况下，不是由 ASP.NET 引擎。 如果其他名称为该文件命名，例如`connectionStrings.txt`，用户无法对其浏览器指向[www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt)并查看该文件的内容 ！


此时`ConfigSections`文件夹应包含三个文件 （请参阅图 4）。 DatabaseConnectionStrings.dev.config 和 databaseConnectionStrings.production.config 文件分别包含开发和生产环境中，连接字符串。 DatabaseConnectionStrings.config 文件包含将由 web 应用程序在运行时的连接字符串信息。 因此，databaseConnectionStrings.config 文件应为与在开发环境中，databaseConnectionStrings.dev.config 文件相同而 databaseConnectionStrings.config 文件应在生产上的相同databaseConnectionStrings.production.config。


[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image10.jpg) 

**图 4**: ConfigSections ([单击以查看实际尺寸的图像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image12.jpg))


现在，我们需要指示`Web.config`要 databaseConnectionStrings.config 文件用于其连接字符串存储区。 打开 `Web.config` 并将现有 `<connectionStrings>` 元素替换为以下内容：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample4.xml)]

`configSource`属性指定相对于的物理路径`Web.config`文件。 如果外部`.config`文件位于与相同的目录`Web.config`然后将此属性设置为的文件名称`.config`文件。 如果它在一个子目录，s databaseConnectionStrings.config，使用这种情况指定使用反斜杠来分隔文件夹和文件的名称，如 ConfigSections\databaseConnectionStrings.config 的子文件夹。

通过这种修改，在开发和生产环境包含相同`Web.config`文件。 现在唯一的区别是 databaseConnectionStrings.config 文件。 将 databaseConnectionStrings.production.config 文件复制到生产环境并将它重命名为 databaseConnectionStrings.config。如果在将来，有对生产数据库连接字符串的更改将需要使到 databaseConnectionStrings.production.config 文件，然后将该文件上载到生产环境中，重命名 databaseConnectionStrings.config。

> [!NOTE]
> 可以指定的任何信息`Web.config`在单独的文件，并使用元素`configSource`属性中引用该文件`Web.config`。


## <a name="summary"></a>总结

数据驱动的应用程序通常在开发和生产环境中使用不同的数据库。 因此，存储在 web 应用程序配置中的数据库连接字符串必须是唯一每个环境。 在本教程中我们介绍了如何确定了生产数据库连接字符串以及维护两种环境中的唯一连接字符串信息的方式。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [连接字符串和配置文件](https://msdn.microsoft.com/library/ms254494.aspx)
- [数据库配置字符串信息 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [移出 Web.config 文件的设置](http://www.asp101.com/tips/index.asp?id=154)
- [技术文档&lt;connectionStrings&gt;元素](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-a-database-vb.md)
> [下一页](configuring-a-website-that-uses-application-services-vb.md)
