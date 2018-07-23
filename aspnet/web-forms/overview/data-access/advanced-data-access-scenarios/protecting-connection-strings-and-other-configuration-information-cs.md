---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
title: 保护连接字符串和其他配置信息 (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET 应用程序通常存储在 Web.config 文件中的配置信息。 此信息的一些敏感，需要保护。 通过 def。...
ms.author: aspnetcontent
ms.date: 08/03/2007
ms.assetid: ad8dd396-30f7-4abe-ac02-a0b84422e5be
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 24a066a4c9d60e3dc1897bd3143b382b876e027c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842216"
---
<a name="protecting-connection-strings-and-other-configuration-information-c"></a>保护连接字符串和其他配置信息 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_CS.zip)或[下载 PDF](protecting-connection-strings-and-other-configuration-information-cs/_static/datatutorial73cs1.pdf)

> ASP.NET 应用程序通常存储在 Web.config 文件中的配置信息。 此信息的一些敏感，需要保护。 默认情况下此文件，不会提供对 Web 站点访问者，但管理员或黑客可能获得对 Web 服务器的文件系统访问并查看该文件的内容。 在本教程中我们了解 ASP.NET 2.0，使我们能够通过加密 Web.config 文件的各个部分来保护敏感信息。


## <a name="introduction"></a>介绍

ASP.NET 应用程序的配置信息通常存储在名为一个 XML 文件`Web.config`。 我们已更新过程中的这些教程`Web.config`少量的时间。 创建时`Northwind`类型中的数据集[第一个教程](../introduction/creating-a-data-access-layer-cs.md)，例如，连接字符串信息已自动添加到`Web.config`中`<connectionStrings>`部分。 在后面[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中，我们手动更新`Web.config`，添加`<pages>`元素，该值指示所有 ASP.NET 页面在我们的项目应使用`DataWebControls`主题。

由于`Web.config`可能包含连接字符串等敏感数据非常重要的内容`Web.config`保持安全和隐藏从未经授权的查看器。 默认情况下，任何 HTTP 请求到的文件`.config`由 ASP.NET 引擎，它将返回处理扩展插件*不提供此类型的页*图 1 所示的消息。 这意味着，访问者不能查看你`Web.config`只需输入文件 s 内容 http://www.YourServer.com/Web.config 到其 s 浏览器地址栏。


[![访问 Web.config 通过浏览器返回此类型的页未处理消息](protecting-connection-strings-and-other-configuration-information-cs/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image1.png)

**图 1**： 访问`Web.config`通过浏览器返回此类型的页未处理消息 ([单击以查看实际尺寸的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image3.png))


但如果攻击者能够找到一些其他攻击，允许她查看你`Web.config`文件 s 内容？ 可以做些什么攻击者使用此信息，并可以执行的步骤来进一步保护敏感信息`Web.config`？ 幸运的是，大多数部分中`Web.config`不包含敏感信息。 什么会造成伤害可以攻击者 perpetrate 如果他们知道默认使用由 ASP.NET 页主题的名称？

某些`Web.config`的部分中，但是，包含敏感信息可能包括连接字符串、 用户名、 密码、 服务器名称、 加密密钥等。 通常在下面找到此信息`Web.config`部分：

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

在本教程中我们将查看用于保护此类敏感配置信息的技术。 我们将会看到，.NET Framework 2.0 版包括，可以以编程方式加密和解密所选的配置节的受保护的配置系统。

> [!NOTE]
> 本教程最后一看 Microsoft 的建议从 ASP.NET 应用程序连接到数据库。 除了加密连接字符串，可以帮助强化通过确保您要连接到安全的方式中的数据库的系统。


## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>步骤 1： 探索 ASP.NET 2.0 s 受保护的配置选项

ASP.NET 2.0 包含受保护的配置系统用于加密和解密配置信息。 这包括可用于以编程方式加密或解密的配置信息的.NET Framework 中的方法。 使用受保护的配置系统[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，它允许开发人员选择使用什么加密实现。

.NET Framework 附带有两个受保护的配置提供程序：

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -使用非对称[RSA 算法](http://en.wikipedia.org/wiki/Rsa)加密和解密。
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -使用 Windows[数据保护 API (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx)加密和解密。

由于受保护的配置系统实现的提供程序设计模式，则可以创建自己的受保护的配置提供程序并将其插入到你的应用程序。 请参阅[实现受保护配置提供程序](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx)有关此过程的详细信息。

在 RSA 和 DPAPI 提供程序对其加密和解密的例程，使用密钥和这些密钥可存储在计算机或用户级别。 计算机级密钥非常适合于其中的 web 应用程序在其专用的服务器上运行，或如果有多个应用程序需要共享的服务器上加密的信息。 用户级密钥是在共享宿主环境，其中在同一台服务器上的其他应用程序不应能够解密您的应用程序受保护的 s 配置节中更安全的选项。

在本教程中我们的示例将使用 DPAPI 提供程序和计算机级别密钥。 具体而言，我们将查看加密`<connectionStrings>`主题中`Web.config`，尽管受保护的配置系统可以用于加密任何大多数`Web.config`部分。 使用用户级密钥或使用 RSA 提供程序上的信息，请在本教程末尾查阅进一步读数部分中的资源。

> [!NOTE]
> `RSAProtectedConfigurationProvider`并`DPAPIProtectedConfigurationProvider`中注册提供程序`machine.config`文件和提供程序名称`RsaProtectedConfigurationProvider`和`DataProtectionConfigurationProvider`分别。 加密或解密我们将需要提供相应的提供程序名称的配置信息时 (`RsaProtectedConfigurationProvider`或`DataProtectionConfigurationProvider`) 而不是实际类型名称 (`RSAProtectedConfigurationProvider`和`DPAPIProtectedConfigurationProvider`)。 您可以找到`machine.config`文件中`$WINDOWS$\Microsoft.NET\Framework\version\CONFIG`文件夹。


## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>步骤 2： 以编程方式加密和解密的配置节

使用几行代码，我们可以加密或解密特定配置部分使用指定的提供程序。 该代码中，我们会很快，只需以编程方式引用相应的配置部分中，调用其`ProtectSection`或`UnprotectSection`方法，，然后调用`Save`方法以持久保存所做的更改。 此外，.NET Framework 包括有用的命令行实用工具，可以加密和解密配置信息。 我们将探讨在步骤 3 中的该命令行实用程序。

为了说明以编程方式保护的配置信息，让 s 创建 ASP.NET 页的按钮可用于加密和解密`<connectionStrings>`主题中`Web.config`。

首先打开`EncryptingConfigSections.aspx`页中`AdvancedDAL`文件夹。 将 TextBox 控件从工具箱拖到设计器中，设置其`ID`属性设置为`WebConfigContents`，将其`TextMode`属性设置为`MultiLine`，并将其`Width`和`Rows`为 95%和 15，属性分别。 此文本框控件将显示的内容`Web.config`使我们能够快速查看是否加密内容。 当然，实际的应用程序将永远不会想要显示的内容`Web.config`。

在文本框中，下面添加两个名为的按钮控件`EncryptConnStrings`和`DecryptConnStrings`。 其文本属性设置为加密连接字符串和解密连接字符串。

此时您的屏幕应类似于图 2。


[![向页面添加一个文本框和两个按钮 Web 控件](protecting-connection-strings-and-other-configuration-information-cs/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image4.png)

**图 2**： 向页面添加一个文本框和两个按钮 Web 控件 ([单击以查看实际尺寸的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image6.png))


接下来，我们需要编写代码，将加载并显示的内容`Web.config`在`WebConfigContents`文本框中第一个页面时加载。 将以下代码添加到页的代码隐藏类。 此代码将添加一个名为方法`DisplayWebConfig`并调用它从`Page_Load`事件处理程序时`Page.IsPostBack`是`false`:


[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample1.cs)]

`DisplayWebConfig`方法使用[`File`类](https://msdn.microsoft.com/library/system.io.file.aspx)若要打开应用程序 s`Web.config`文件[`StreamReader`类](https://msdn.microsoft.com/library/system.io.streamreader.aspx)其内容读入字符串，将[`Path`类](https://msdn.microsoft.com/library/system.io.path.aspx)生成的物理路径`Web.config`文件。 这三个类在中找到[`System.IO`命名空间](https://msdn.microsoft.com/library/system.io.aspx)。 因此，需要将添加`using``System.IO`语句或顶部的代码隐藏类，或者，这些类具有的名称的前缀`System.IO.`。

接下来，我们需要添加两个 Button 控件的事件处理程序`Click`事件，并添加所需的代码来加密和解密`<connectionStrings>`部分计算机级密钥使用 DPAPI 提供程序。 从设计器中，双击要添加的按钮的每个`Click`代码隐藏中的事件处理程序类，然后添加以下代码：


[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample2.cs)]

在两个事件处理程序中使用的代码是几乎完全相同。 它们都首先获取当前应用程序有关的信息`Web.config`文件通过[`WebConfigurationManager`类](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx)s [ `OpenWebConfiguration`方法](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)。 此方法返回指定的虚拟路径的 web 配置文件。 下一步，`Web.config`文件 s`<connectionStrings>`通过访问部分[`Configuration`类](https://msdn.microsoft.com/library/system.configuration.configuration.aspx)s [ `GetSection(sectionName)`方法](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)，它将返回[ `ConfigurationSection` ](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx)对象。

`ConfigurationSection`对象中包含[`SectionInformation`属性](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx)，它提供的其他信息和功能有关的配置节。 作为上面所示的代码，我们可以确定是否通过检查加密配置节`SectionInformation`属性的`IsProtected`属性。 此外，可以加密或解密通过部分`SectionInformation`属性 s`ProtectSection(provider)`和`UnprotectSection`方法。

`ProtectSection(provider)`方法接受作为输入一个字符串，指定要加密时使用的受保护的配置提供程序的名称。 在中`EncryptConnString`s 按钮事件处理程序，我们将传递到 DataProtectionConfigurationProvider`ProtectSection(provider)`方法，以便使用 DPAPI 提供程序。 `UnprotectSection`方法可以确定的提供程序用于加密配置节，因此不需要任何输入参数。

在调用`ProtectSection(provider)`或`UnprotectSection`方法时，必须调用`Configuration`对象 s [ `Save`方法](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx)保存所做的更改。 已加密或解密的配置信息并保存更改，我们调用后`DisplayWebConfig`加载已更新`Web.config`到 TextBox 控件的内容。

输入上面的代码后, 对其进行测试，请访问`EncryptingConfigSections.aspx`通过浏览器的页。 您最初应看到列出的内容的页面`Web.config`与`<connectionStrings>`以纯文本形式显示的部分 （参见图 3）。


[![向页面添加一个文本框和两个按钮 Web 控件](protecting-connection-strings-and-other-configuration-information-cs/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image7.png)

**图 3**： 向页面添加一个文本框和两个按钮 Web 控件 ([单击以查看实际尺寸的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image9.png))


现在，单击加密连接字符串按钮。 如果启用请求验证，则返回从发布标记`WebConfigContents`文本框中将生成`HttpRequestValidationException`，其中显示消息，具有潜在危险`Request.Form`从客户端检测到值。 请求验证，启用 ASP.NET 2.0 中默认情况下，它禁止将包含未编码 HTML 的回发，设计用于帮助防止脚本注入攻击。 可以在页面或应用程序级别禁用此检查。 若要将其关闭此页，设置`ValidateRequest`设置为`false`中`@Page`指令。 `@Page`指令找到页面 s 声明性标记顶部。


[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample3.aspx)]

有关详细信息请求验证，其用途，如何在页和应用程序级别，以及如何为 HTML 编码的标记如禁用它，请参阅[请求验证-阻止脚本攻击](../../../../whitepapers/request-validation.md)。

禁用之后的页请求验证，请尝试再次单击加密连接字符串按钮。 将回发时，访问该配置文件并将其`<connectionStrings>`加密使用 DPAPI 提供程序的部分。 然后，更新文本框以显示新`Web.config`内容。 如图 4 所示，`<connectionStrings>`信息都会进行加密。


[![单击加密连接字符串按钮加密&lt;connectionString&gt;部分](protecting-connection-strings-and-other-configuration-information-cs/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image10.png)

**图 4**： 单击加密连接字符串按钮加密`<connectionString>`部分 ([单击以查看实际尺寸的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image12.png))


加密`<connectionStrings>`我的计算机上生成的部分将跟踪，尽管部分中的内容`<CipherData>`为简便起见已移除元素：


[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>`元素指定用于执行加密的提供程序 (`DataProtectionConfigurationProvider`)。 此信息由`UnprotectSection`方法时单击解密连接字符串按钮。


当从访问连接字符串信息时`Web.config`，无论是由我们编写的从 SqlDataSource 控件或从我们的类型化数据集在 Tableadapter 的自动生成的代码-会自动解密。 简单地说，我们不需要添加任何额外的代码或逻辑来解密加密`<connectionString>`部分。 若要演示此操作，请访问之前的教程之一在此时，如基本报告部分的简单显示教程 (`~/BasicReporting/SimpleDisplay.aspx`)。 如图 5 所示，教程适用于完全按照我们期望的那样，指示加密的连接字符串信息由 ASP.NET 页时被自动解密。


[![数据访问层自动解密的连接字符串信息](protecting-connection-strings-and-other-configuration-information-cs/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image13.png)

**图 5**： 数据访问层自动解密连接字符串信息 ([单击以查看实际尺寸的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image15.png))


若要还原`<connectionStrings>`部分回其纯文本表示形式中，单击解密连接字符串按钮。 应在回发时请参阅中的连接字符串`Web.config`以纯文本。 此时您的屏幕应看起来像第一次访问此页 （请参阅图 3 中） 时。

## <a name="step-3-encrypting-configuration-sections-usingaspnetregiisexe"></a>步骤 3： 加密使用的配置节`aspnet_regiis.exe`

.NET Framework 包括命令行工具中的各种`$WINDOWS$\Microsoft.NET\Framework\version\`文件夹。 在中[使用 SQL 缓存依赖项](../caching-data/using-sql-cache-dependencies-cs.md)教程中，例如，我们了解了使用`aspnet_regsql.exe`命令行工具，用于添加 SQL 缓存依赖项所需的基础结构。 此文件夹中的另一个有用的命令行工具是[ASP.NET IIS 注册工具 (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)。 正如其名，ASP.NET IIS 注册工具主要用于向 Microsoft 的专业级 Web 服务器，IIS 注册 ASP.NET 2.0 应用程序。 除了其与 IIS 相关的功能，ASP.NET IIS 注册工具还可用来加密或解密指定的配置节中`Web.config`。

以下语句显示了用来加密配置节的常规语法`aspnet_regiis.exe`命令行工具：


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample5.cmd)]

*部分*是配置节进行加密 （如 connectionStrings)，*物理\_directory*是 web 应用程序的根目录的完整的物理路径和*提供程序*是受保护的配置提供程序 （如 DataProtectionConfigurationProvider) 使用的名称。 或者，如果在 IIS 中注册 web 应用程序可以输入的虚拟路径而不是在物理路径中使用以下语法：


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample6.cmd)]

以下`aspnet_regiis.exe`示例加密`<connectionStrings>`部分使用 DPAPI 提供程序和计算机级别的密钥：


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample7.cmd)]

同样，`aspnet_regiis.exe`命令行工具可用于解密的配置节。 而不是使用`-pef`切换，请使用`-pdf`(或代替`-pe`，使用`-pd`)。 另请注意，提供程序名称时不需要解密。


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample8.cmd)]

> [!NOTE]
> 因为我们要使用 DPAPI 提供程序，后者使用特定于的计算机的键时，必须运行`aspnet_regiis.exe`从您的浏览器提供从其在同一台计算机。 例如，如果从本地开发计算机上运行此命令行程序，然后将加密的 Web.config 文件上载到生产服务器，在生产服务器将不能对连接字符串信息解密加密之后使用特定于你的开发计算机密钥。 RSA 提供程序不具有此限制，因为可以将 RSA 密钥导出到另一台计算机。


## <a name="understanding-database-authentication-options"></a>了解数据库身份验证选项

任何应用程序可以发出之前`SELECT`， `INSERT`， `UPDATE`，或`DELETE`到 Microsoft SQL Server 数据库，数据库的查询必须首先标识请求者。 此过程被称为*身份验证*和 SQL Server 提供的身份验证的两种方法：

- **Windows 身份验证**-在其下运行应用程序的过程用于与数据库通信。 当运行 ASP.NET 应用程序通过 Visual Studio 2005 的 ASP.NET Development Server，ASP.NET 应用程序假定当前登录用户的标识。 对于 ASP.NET 应用程序在 Microsoft Internet 信息服务器 (IIS)，ASP.NET 应用程序通常采用的标识`domainName``\MachineName`或`domainName``\NETWORK SERVICE`，尽管这可以自定义。
- **SQL 身份验证**的形式进行身份验证的凭据提供用户 ID 和密码值。 使用 SQL 身份验证连接字符串中提供的用户 ID 和密码。

Windows 身份验证通过 SQL 身份验证中都是首选的因为它是更安全。 使用 Windows 身份验证连接字符串是免费的用户名和密码从和 web 服务器和数据库服务器驻留在两个不同的计算机上，如果凭据不通过网络以纯文本发送。 使用 SQL 身份验证，但是，身份验证凭据是硬编码连接字符串中并从 web 服务器传输到数据库服务器以纯文本。

这些教程已使用 Windows 身份验证。 您可以告知正在检查连接字符串使用的身份验证模式。 中的连接字符串`Web.config`的教程已：

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Integrated Security = True 和缺少的用户名和密码指示使用 Windows 身份验证。 在某些连接字符串的术语受信任连接 = Yes 或集成的安全性 = SSPI 使用而不是集成安全性 = True，但所有这三个指示使用 Windows 身份验证。

下面的示例显示了使用 SQL 身份验证的连接字符串。 请注意在连接字符串内嵌入的凭据：

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

假设攻击者有权查看您的应用程序 s`Web.config`文件。 如果您使用 SQL 身份验证连接到的数据库，则可以通过 Internet 访问，攻击者可以使用此连接字符串以连接到数据库通过 SQL Management Studio 或从自己的网站上的 ASP.NET 页。 若要帮助缓解此威胁，加密中的连接字符串信息`Web.config`使用受保护的配置系统。

> [!NOTE]
> 有关不同类型的 SQL Server 中提供的身份验证的详细信息，请参阅[Building Secure ASP.NET Applications： 身份验证、 授权和安全通信](https://msdn.microsoft.com/library/aa302392.aspx)。 有关其他连接字符串示例演示 Windows 和 SQL 身份验证语法之间的差异，请参阅[ConnectionStrings.com](http://www.connectionstrings.com/)。


## <a name="summary"></a>总结

默认情况下，文件的工具`.config`不能通过浏览器访问 ASP.NET 应用程序中的扩展。 不返回这些类型的文件，因为它们可能包含敏感信息，例如数据库连接字符串、 用户名和密码，依次类推。 .NET 2.0 中的受保护的配置系统可帮助进一步保护敏感信息通过允许指定的配置节进行加密。 有两个内置的受保护的配置提供程序： 一个使用 RSA 算法，另一个使用 Windows 数据保护 API (DPAPI)。

在本教程中我们介绍了如何加密和解密使用 DPAPI 提供程序的配置设置。 此操作可以完成这两种以编程方式，在步骤 2 中所示，还通过`aspnet_regiis.exe`步骤 3 中所涉及的命令行工具。 使用用户级密钥或改为使用 RSA 提供程序的详细信息，请参阅更多参考资料部分中的资源。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [构建安全的 ASP.NET 应用程序： 身份验证、 授权和安全通信](https://msdn.microsoft.com/library/aa302392.aspx)
- [加密 ASP.NET 2.0 中的配置信息的应用程序](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [加密`Web.config`ASP.NET 2.0 中的值](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [如何： 加密 ASP.NET 2.0 中的配置节使用 DPAPI](https://msdn.microsoft.com/library/ms998280.aspx)
- [如何： 加密 ASP.NET 2.0 中的配置节，可使用 RSA](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0 中的配置 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 数据保护](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和 Randy Schmidt。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
> [下一页](debugging-stored-procedures-cs.md)
