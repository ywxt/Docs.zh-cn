---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: 配置文件、 主题和 Web 部件 |Microsoft Docs
author: microsoft
description: 有配置中的重大更改和 ASP.NET 2.0 中的检测。 新的 ASP.NET 配置 API 允许进行拉取请求的配置更改...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: 98559c2a378c72bc5664faafe5436753050b574f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830888"
---
<a name="profiles-themes-and-web-parts"></a>配置文件、 主题和 Web 部件
====================
by [Microsoft](https://github.com/microsoft)

> 有配置中的重大更改和 ASP.NET 2.0 中的检测。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，许多新的配置设置存在允许对新的配置和检测。


ASP.NET 2.0 表示实质性改善的区域中的个性化的网站。 除了成员身份功能我们已涵盖，ASP.NET 配置文件、 主题和 Web 部件显著提高在网站中的个性化设置。

## <a name="aspnet-profiles"></a>ASP.NET 配置文件

ASP.NET 配置文件是类似于会话。 不同之处在于，配置文件是永久性的而关闭浏览器时，会话会丢失。 会话和配置文件之间的另一个明显区别是，配置文件都强类型，因此您提供 IntelliSense 在开发过程中。

计算机配置文件或应用程序的 web.config 文件中定义了一个配置文件。 （您不能定义一个配置文件的子文件夹 web.config 文件中。）下面的代码定义要首先存储网站访问者和姓氏的配置文件。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

配置文件属性的默认数据类型为 System.String。 在上述示例中，不指定任何数据类型。 因此 FirstName 和 LastName 属性均为类型字符串。 正如前面提到，强类型属性的配置文件。 下面的代码将新属性添加的类型为 Int32 的期限。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

配置文件通常适用于 ASP.NET 窗体身份验证。 每个用户时与窗体身份验证结合使用，具有单独的配置文件与其用户 id。 但是，还有可能允许匿名应用程序使用中的配置文件使用&lt;anonymousIdentification&gt;以及在配置文件中的元素**allowAnonymous**作为属性如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

当匿名用户浏览站点时，ASP.NET 创建的实例**ProfileCommon**用户。 此配置文件使用存储在 cookie 中的浏览器上的唯一 ID 来将用户标识为唯一访问者。 这样一来，可以存储用户的浏览以匿名方式配置文件的信息。

## <a name="profile-groups"></a>配置文件组

它是可能的配置文件的组属性。 通过对分组的属性，就可以模拟的特定应用程序的多个配置文件。

下面的配置配置两个组; 的 FirstName 和 LastName 属性购买者和潜在客户。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

这样，它将可以对特定组中，如下所示设置属性：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>存储复杂对象

到目前为止，我们已经介绍的示例已在配置文件中存储简单数据类型。 还有可能通过指定序列化使用的方法的配置文件中存储复杂数据类型**serializeAs**属性，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

在这种情况下，类型为 PurchaseInvoice。 PurchaseInvoice 类需要标记为可序列化，并且可以包含任意数量的属性。 例如，如果 PurchaseInvoice 具有一个名为属性**NumItemsPurchased**，可以参考代码中的该属性，如下所示：

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>配置文件继承

就可以创建多个应用程序中使用的配置文件。 通过创建从 ProfileBase 派生而来的配置文件类，可以通过重用多个应用程序中的配置文件**继承**属性，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

在此情况下，该类**PurchasingProfile**看起来如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>配置文件提供程序

ASP.NET 配置文件使用的提供程序模型。 默认提供程序将信息存储在应用中的 SQL Server Express 数据库\_使用 SqlProfileProvider 提供程序的 Web 应用程序数据文件夹。 如果数据库不存在，ASP.NET 将自动创建它时尝试将信息存储在配置文件。

在某些情况下，但是，你可能想要开发自己的配置文件提供程序。 ASP.NET 配置文件功能使你能够轻松使用不同的提供程序。

创建自定义配置文件提供程序时：

- 您需要将配置文件信息存储在数据源，如在 FoxPro 数据库或 Oracle 数据库中，不支持.NET Framework 附带的配置文件提供程序。
- 需要管理使用不同于使用.NET Framework 附带的提供程序的数据库架构的数据库架构的配置文件信息。 常见示例是您想要将配置文件信息集成使用现有 SQL Server 数据库中的用户数据。

### <a name="required-classes"></a>所需的类

若要实现配置文件提供程序，您可以创建继承 System.Web.Profile.ProfileProvider 抽象类的类。 **ProfileProvider**抽象类又继承 System.Configuration.SettingsProvider 抽象类，该类继承 System.Configuration.Provider.ProviderBase 抽象类。 由于此继承链，除了的所需的成员**ProfileProvider**类，必须实现的所需的成员**SettingsProvider**和**ProviderBase**类。

下表描述的属性和方法必须从实现**ProviderBase**， **SettingsProvider**，并**ProfileProvider**抽象类。

### <a name="providerbase-members"></a>ProviderBase 成员

| **成员** | **说明** |
| --- | --- |
| Initialize 方法 | 接受的输入提供程序实例的名称和配置设置的 NameValueCollection。 用于设置选项和提供程序实例，其中包括特定于实现的值和选项的计算机配置或 Web.config 文件中指定的属性值。 |

### <a name="settingsprovider-members"></a>SettingsProvider 成员

| **成员** | **说明** |
| --- | --- |
| 应用程序名称属性 | 与每个配置文件存储在应用程序名称。 配置文件提供程序使用的应用程序名称来存储单独的每个应用程序配置文件信息。 这使多个 ASP.NET 应用程序使用相同的数据源不发生冲突，如果在不同的应用程序中创建相同的用户名。 或者，多个 ASP.NET 应用程序可以共享配置文件数据源指定相同的应用程序名称。 |
| GetPropertyValues 方法 | 将作为输入一 SettingsContext 和 SettingsPropertyCollection 对象。 **SettingsContext**提供了有关用户的信息。 可以使用作为主键的信息来检索用户的配置文件属性信息。 使用**SettingsContext**要获取的用户名以及用户是否已经过身份验证或匿名对象。 **SettingsPropertyCollection**包含 SettingsProperty 对象的集合。 每个**SettingsProperty**对象提供的名称和类型的属性以及其他信息，例如属性和属性是只读的默认值。 **GetPropertyValues**方法使用的基于 SettingsPropertyValue 对象填充 SettingsPropertyValueCollection **SettingsProperty**对象作为输入提供。 指定用户数据源中的值分配给 PropertyValue 属性为每个**SettingsPropertyValue**返回对象和整个集合。 调用该方法还 LastActivityDate 值更新指定的用户配置文件为当前日期和时间。 |
| SetPropertyValues 方法 | 接受的输入**SettingsContext**和一个**SettingsPropertyValueCollection**对象。 **SettingsContext**提供了有关用户的信息。 可以使用作为主键的信息来检索用户的配置文件属性信息。 使用**SettingsContext**要获取的用户名以及用户是否已经过身份验证或匿名对象。 **SettingsPropertyValueCollection**包含一系列**SettingsPropertyValue**对象。 每个**SettingsPropertyValue**对象提供名称、 类型和值的属性以及其他信息，例如属性和属性是只读的默认值。 **SetPropertyValues**方法更新指定用户的数据源中的配置文件属性值。 调用此方法还会更新**LastActivityDate** LastUpdatedDate 的和的值为当前日期和时间的指定的用户配置文件。 |

### <a name="profileprovider-members"></a>ProfileProvider 成员

| **成员** | **说明** |
| --- | --- |
| DeleteProfiles 方法 | 将作为输入的用户的字符串数组名称，并从数据源的指定名称的所有配置文件信息和属性值中删除应用程序名称与匹配之处**ApplicationName**属性值。 如果您的数据源支持事务，建议在事务中包括所有删除操作和回滚事务，如果任何删除操作失败引发异常。 |
| DeleteProfiles 方法 | 将作为输入的 ProfileInfo 集合对象，并从数据源中删除每个配置文件的所有配置文件信息和属性值的应用程序名称与匹配之处**ApplicationName**属性值。 如果您的数据源支持事务，建议的事务中包含所有删除操作和回滚事务并引发异常，如果任何删除操作失败。 |
| DeleteInactiveProfiles 方法 | 作为输入 ProfileAuthenticationOption 值和 DateTime 对象和删除从数据源配置文件的所有信息和属性值，其中，上次活动日期小于或等于指定的日期和时间，且应用程序名称与匹配**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，或所有配置文件将被删除。 如果您的数据源支持事务，建议的事务中包含所有删除操作和回滚事务并引发异常，如果任何删除操作失败。 |
| GetAllProfiles 方法 | 接受的输入**ProfileAuthenticationOption**值、 一个整数，指定的页索引、 一个整数，指定页大小和对一个整数，它将设置为配置文件的总计数的引用。 返回包含 ProfileInfoCollection **ProfileInfo**对象的应用程序名称与相匹配的数据源中的所有配置文件**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，还是要返回所有配置文件。 返回的结果**GetAllProfiles**方法受到约束的页索引和页大小值。 页面大小值指定的最大数目**ProfileInfo**对象中返回**ProfileInfoCollection**。 页的索引值指定哪一页的结果返回，其中 1 表示第一页。 总记录数的参数是一个输出参数 (可以使用**ByRef**在 Visual Basic 中) 设置为配置文件的总数。 例如，如果数据存储区包含 13 个应用程序的配置文件和页面索引值为 2，5，页面大小**ProfileInfoCollection**返回包含第六到第十个配置文件。 该方法返回时，总记录数的值设置为 13。 |
| GetAllInactiveProfiles 方法 | 接受的输入**ProfileAuthenticationOption**值， **DateTime**对象、 一个整数，指定的页索引、 一个整数，指定页面大小，并将设置一个整数的引用为配置文件的总计数。 返回**ProfileInfoCollection** ，其中包含**ProfileInfo**对象的上次活动日期小于或等于指定的数据源中的所有配置文件**日期时间**和应用程序名称与匹配之处**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，还是要返回所有配置文件。 返回的结果**GetAllInactiveProfiles**方法受到约束的页索引和页大小值。 页面大小值指定的最大数目**ProfileInfo**对象中返回**ProfileInfoCollection**。 页的索引值指定哪一页的结果返回，其中 1 表示第一页。 总记录数的参数是一个输出参数 (可以使用**ByRef**在 Visual Basic 中) 设置为配置文件的总数。 例如，如果数据存储区包含 13 个应用程序的配置文件和页面索引值为 2，5，页面大小**ProfileInfoCollection**返回包含第六到第十个配置文件。 该方法返回时，总记录数的值设置为 13。 |
| FindProfilesByUserName 方法 | 接受的输入**ProfileAuthenticationOption**值，包含用户名称、 一个整数，指定的页索引、 一个整数，指定页大小和对一个整数，它将设置为的总计数的引用的字符串配置文件。 返回**ProfileInfoCollection** ，其中包含**ProfileInfo**对象数据中的所有配置文件的源的用户名与指定的用户名匹配之处和应用程序名称与相匹配**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，还是要返回所有配置文件。 如果您的数据源支持其他搜索功能，如通配符字符，您可以更广泛的搜索功能的用户名称。 返回的结果**FindProfilesByUserName**方法受到约束的页索引和页大小值。 页面大小值指定的最大数目**ProfileInfo**对象中返回**ProfileInfoCollection**。 页的索引值指定哪一页的结果返回，其中 1 表示第一页。 总记录数的参数是一个输出参数 (可以使用**ByRef**在 Visual Basic 中) 设置为配置文件的总数。 例如，如果数据存储区包含 13 个应用程序的配置文件和页面索引值为 2，5，页面大小**ProfileInfoCollection**返回包含第六到第十个配置文件。 该方法返回时，总记录数的值设置为 13。 |
| FindInactiveProfilesByUserName 方法 | 接受的输入**ProfileAuthenticationOption**值，包含用户名的字符串**DateTime**对象、 一个整数，指定的页索引、 一个整数，指定页大小和引用为一个整数，将设置为配置文件的总计数。 返回**ProfileInfoCollection** ，其中包含**ProfileInfo**中上次活动日期所在的数据源的用户名与指定的用户名相匹配的所有配置文件的对象小于或等于指定**DateTime**，并在其中应用程序名称匹配**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，还是要返回所有配置文件。 如果您的数据源支持其他搜索功能，如通配符字符，您可以更广泛的搜索功能的用户名称。 返回的结果**FindInactiveProfilesByUserName**方法受到约束的页索引和页大小值。 页面大小值指定的最大数目**ProfileInfo**对象中返回**ProfileInfoCollection**。 页的索引值指定哪一页的结果返回，其中 1 表示第一页。 总记录数的参数是一个输出参数 (可以使用**ByRef**在 Visual Basic 中) 设置为配置文件的总数。 例如，如果数据存储区包含 13 个应用程序的配置文件和页面索引值为 2，5，页面大小**ProfileInfoCollection**返回包含第六到第十个配置文件。 该方法返回时，总记录数的值设置为 13。 |
| GetNumberOfInActiveProfiles 方法 | 接受的输入**ProfileAuthenticationOption**值和一个**DateTime**对象，并在其中，上次活动日期是小于或等于指定数据源中返回的所有配置文件计数**日期时间**和应用程序名称与匹配之处**ApplicationName**属性值。 **ProfileAuthenticationOption**参数指定是否仅匿名配置文件，只有经过身份验证配置文件，或所有配置文件是要进行计数。 |

### <a name="applicationname"></a>ApplicationName

由于配置文件提供程序存储单独为每个应用程序的配置文件信息，必须确保数据架构，包括应用程序名称，查询和更新还包括应用程序名称。 例如，下面的命令用于从基于用户名称和配置文件是否是匿名的数据库中检索属性值，并确保**ApplicationName**值包含在查询中。

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET 主题

## <a name="what-are-aspnet-20-themes"></a>ASP.NET 2.0 主题有哪些？

Web 应用程序的最重要方面之一在站点之间是一致的外观。 ASP.NET 1.x 开发人员通常使用级联样式表 (CSS) 来实现一致的外观。 ASP.NET 2.0 主题显著改进 CSS 因为它们使 ASP.NET 开发人员能够定义 ASP.NET 服务器控件的 HTML 元素的外观。 ASP.NET 主题可以应用于单个控件、 特定的 Web 页上或整个 Web 应用程序。 如果需要映像，主题使用 CSS 文件、 一个可选外观文件和一个可选的映像目录的组合。 外观文件控制 ASP.NET 服务器控件的可视外观。

## <a name="where-are-themes-stored"></a>在哪里？ 主题存储

主题的存储位置的位置不同在其作用域的基础。 可以应用于任何应用程序的主题存储在以下文件夹中：

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

特定于特定应用程序的主题存储在`App\_Themes\<Theme\_Name>`目录中的网站的根。

> [!NOTE]
> 外观文件仅应修改会影响外观的服务器控件属性。

全局主题是可以应用于任何应用程序或 Web 服务器上运行的网站上的主题。 默认情况下是在 v2.x.xxxxx 目录内的 ASP.NETClientfiles\Themes 目录中存储这些主题。 或者，可以将主题文件移动到 aspnet\_客户端/系统\_web / [version] /Themes/ [主题\_名称] 中您的网站的根文件夹。

只能对应用程序文件驻留在其中应用特定于应用程序的主题。 这些文件存储在`App\_Themes/<theme\_name>`目录中的网站的根。

## <a name="the-components-of-a-theme"></a>主题的组件

主题由一个或多个 CSS 文件、 一个可选外观文件和一个可选的 Images 文件夹组成。 CSS 文件可以是任何您想 （即 default.css 或 theme.css 等），且必须是主题文件夹的根目录中的名称。 CSS 文件用于定义普通 CSS 类和特定的选择器的属性。 要应用于页面元素的 CSS 类之一**CSSClass**使用属性。

外观文件是一个包含 ASP.NET 服务器控件的属性定义的 XML 文件。 下面列出的代码是一个示例外观文件。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**图 1**下显示了一个小的 ASP.NET 页面浏览而无需应用主题。 **图 2**并应用主题中显示的同一文件。 通过 CSS 文件配置的背景色和文本颜色。 使用上面所列的外观文件配置按钮和文本框的外观。


![无主题](profiles-themes-and-web-parts/_static/image1.gif)

**图 1**： 无主题


![应用主题](profiles-themes-and-web-parts/_static/image2.gif)

**图 2**： 应用主题


上面列出的外观文件定义所有文本框控件和按钮控件的默认的外观。 这意味着，每个 TextBox 控件和在网页中插入的按钮控件将采用此外观。 您还可以定义可应用于使用这些控件的特定实例的外观**SkinID**控件的属性。

下面的代码定义一个按钮控件的外观。 只有按钮控件**SkinID**的属性**转**需要的外观的外观。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

只能有一个每个服务器控件类型的默认外观。 如果需要其他的外观，您应使用 SkinID 属性。

## <a name="applying-themes-to-pages"></a>应用主题到网页

可以使用以下方法之一应用主题：

- 在中&lt;页面&gt;web.config 文件的元素
- 在@Page页面的指令
- 以编程方式

## <a name="applying-a-theme-in-the-configuration-file"></a>应用配置文件中的主题

若要应用的应用程序配置文件中的一个主题，请使用以下语法：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

此处指定的主题名称必须匹配主题文件夹的名称。 此文件夹可以存在的任何一种方法在本课程前面提到的位置。 如果你尝试应用主题不存在，将发生配置错误。

## <a name="applying-a-theme-in-the-page-directive"></a>应用页面指令中的主题

您还可以应用在 @ 页面指令中的一个主题。 此方法，可将特定页面的主题。

若要将应用中的一个主题@Page指令，请使用以下语法：

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

再次重申，正如前面提到此处指定的主题必须与匹配的主题文件夹。 如果你尝试应用主题不存在，将发生生成失败。 Visual Studio 还将突出显示该属性，并通知你存在任何此类主题。

## <a name="applying-a-theme-programmatically"></a>以编程方式应用主题

若要以编程方式应用主题，必须指定**主题**属性中的页**页面\_PreInit**方法。

若要以编程方式应用主题，请使用以下语法：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

它是必要应用 PreInit 方法，因为页面生命周期中的主题。 如果该时间点后将其应用，页主题将已应用运行时和更改在该点为时已晚生命周期中。 如果应用不存在，一个主题**HttpException**时发生。 以编程方式应用主题时，如果任何服务器控件已指定 SkinID 属性，将发生生成警告。 此警告旨在通知您以声明方式应用任何主题，则可以忽略它。

## <a name="exercise-1--applying-a-theme"></a>练习 1： 应用主题

在此练习中，您将应用到网站上的 ASP.NET 主题。

> [!IMPORTANT]
> 如果使用 Microsoft Word 来外观文件中输入信息，请确保你不会替代正则引号弯引号。 弯引号将导致外观文件出现问题。

1. 创建一个新的 ASP.NET 网站。
2. 右键单击解决方案资源管理器中的项目，然后选择添加新项。
3. 从文件的列表中选择 Web 配置文件，并单击添加。
4. 右键单击解决方案资源管理器中的项目，然后选择添加新项。
5. 选择外观文件，然后单击添加。
6. 单击是当询问您可能要将应用内的文件放置\_主题文件夹。
7. 右键单击 SkinFile 文件夹应用内\_在解决方案资源管理器中的主题文件夹，然后选择添加新项。
8. 从文件的列表中选择样式表并单击添加。 您现在拥有的所有实现您的新主题所需文件。 但是，Visual Studio 具有名为您的主题文件夹 SkinFile。 右键单击该文件夹并将名称更改为 CoolTheme。
9. 打开 SkinFile.skin 文件并添加以下代码文件的末尾： 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. 保存 SkinFile.skin 文件。
11. 打开 StyleSheet.css。
12. 使用以下内容替换所有中它的文本： 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. 保存 StyleSheet.css 文件。
14. 打开 Default.aspx 页。
15. 添加 TextBox 控件和一个 Button 控件。
16. 保存页。 现在，浏览 Default.aspx 页。 它应显示为普通的 Web 窗体。
17. 打开 web.config 文件。
18. 添加正下方打开以下`<system.web>`标记： 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. 保存 web.config 文件。 现在，浏览 Default.aspx 页。 它应显示与应用的主题。
20. 如果尚未打开，请在 Visual Studio 中打开 Default.aspx 页。
21. 选择按钮。
22. 更改**SkinID**转到的属性。 请注意，Visual Studio 为按钮控件提供了一个使用有效的 SkinID 值的下拉列表。
23. 保存页。 现在再次预览您的浏览器中的页。 该按钮现在应显示"转到"，并应会在外观更大。

使用**SkinID**属性，您可以轻松地配置不同外观的特定类型的服务器控件的不同实例。

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme 属性

到目前为止，我们介绍了仅应用主题使用主题属性。 当使用主题属性，外观文件将覆盖服务器控件的任何声明性设置。 例如，在练习 1 中，指定的按钮控件的"转"SkinID 并更改按钮的文本为"go"。 您可能已经注意到，在设计器中的按钮的 Text 属性设置为"按钮"，但主题重写的。 主题将始终覆盖在设计器中的任何属性设置。

如果你想要能够重写中的主题外观文件与定义的属性中指定属性设计器中，可以使用**StyleSheetTheme**而不是主题属性的属性。 StyleSheetTheme 属性是与主题属性相同，只不过它不会覆盖所有显式属性设置类似主题属性执行的操作。

若要了解此操作，请从在练习 1 中的项目中打开 web.config 文件，然后更改`<pages>`以下元素：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

现在，浏览 Default.aspx 页，将看到按钮控件重新具有"按钮"的文本属性。 这是因为在设计器中的显式属性设置会替代由转 SkinID 设置的 Text 属性。

## <a name="overriding-themes"></a>重写主题

应用由应用程序中具有相同名称的主题可以替代全局主题\_主题的应用程序文件夹。 但是，该主题中，则返回 true 的替代方案不应用。 如果运行时遇到的应用中的主题文件\_主题文件夹中，它将应用使用这些文件的主题，并且将忽略全局主题。

StyleSheetTheme 属性是可重写，并且可以覆盖在代码中，如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Web 部件

ASP.NET Web 部件是网页的一组集成的控件，用于创建网站使最终用户可以修改内容、 外观和行为直接从浏览器。 可以应用所做的修改，该站点上的所有用户或单个用户。 当用户修改页面和控件时，可以保存这些设置，以便一个名为个性化设置功能在将来的浏览器会话之间保留用户的个人首选项。 这些 Web 部件功能意味着开发人员可以使最终用户可以动态地个性化的 Web 应用程序，而无需开发人员或管理员干预。

使用 Web 部件控件集，您作为开发人员可以允许最终用户到：

- 对页面内容进行个性化设置。 用户可以向页面添加新的 Web 部件控件、 将其删除，隐藏它们，或它们像普通窗口最小化。
- 个性化页面布局。 用户可以将 Web 部件控件拖到另一个区域，在页上，或更改其外观、 属性和行为。
- 导出和导入控件。 用户可以导入或导出 Web 部件控件中使用设置的其他页面或站点，同时保留属性、 外观和甚至在控件中的数据。 这会减少最终用户的数据输入和配置要求。
- 创建连接。 用户可以建立控件之间的连接，以便例如，图表控件可以显示的数据图形，股票行情自动收录器控件中。 用户可以个性化设置不仅连接本身，但外观和图表控件显示数据的方式的详细信息。
- 管理和自定义网站级别的设置。 经过授权的用户可以配置站点级设置，确定谁可以访问站点或页面、 基于角色的访问权限设置为控件，依次类推。 例如，管理角色中的用户可以设置 Web 部件控件共享的所有用户，并禁止用户不是管理员对共享的控件。

通常将使用三种方式之一中的 Web 部件： 创建的使用 Web 部件控件的页、 创建单独的 Web 部件控件，或创建完整的可个性化的 Web 应用程序，如门户。

## <a name="page-development"></a>页面开发

页面开发人员可以使用可视化设计工具，如 Microsoft Visual Studio 2005 创建使用 Web 部件页。 在使用一种工具，如 Visual Studio 是 Web 部件控件集的一个优点提供拖放的创建和配置的可视设计器中的 Web 部件控件的功能。 例如，您可以使用设计器将 Web 部件区域或 Web 部件编辑器控件，拖到设计图面，然后配置向右调整控件在设计器中使用用户界面提供的 Web 部件控件集。 这可以加速开发的 Web 部件应用程序并减少您必须编写的代码量。

## <a name="control-development"></a>控件开发

作为 Web 部件控件，包括标准 Web 服务器控件、 自定义服务器控件和用户控件，可以使用任何现有的 ASP.NET 控件。 对于您的环境的最大的编程控制，还可以创建从 web 部件类派生的自定义 Web 部件控件。 对于单个 Web 部件控件的开发，您将通常创建用户控件，将其用作 Web 部件控件，或者开发一个自定义 Web 部件控件。

作为开发自定义 Web 部件控件的示例，可以创建一个控件来提供任何其他可能可用于包作为可个性化的 Web 部件控件的 ASP.NET 服务器控件提供的功能： 日历、 列表、 财务信息新闻、 计算器、 多格式文本控件的更新内容，可编辑网格，连接到数据库，动态更新其显示器或天气和旅行信息的图表。 如果与您的控件提供可视化设计器，然后使用 Visual Studio 任何页面开发人员可以只需将控件拖到 Web 部件区域并在设计时将其配置，而无需编写其他代码。

个性化设置是 Web 部件功能的基础。 它使用户能够修改-或个性化设置布局、 外观和行为的页面上的 Web 部件控件。 个性化的设置很长： 而不仅仅是当前的浏览器会话期间保留 （与视图状态一样），但还会在长期存储，以便为将来的浏览器的会话保存用户的设置。 默认情况下，为 Web 部件页启用个性化设置。

UI 结构组件依赖于个性化设置，并提供核心结构和服务所需的所有 Web 部件控件。 每个 Web 部件页上所需的一个 UI 结构组件是 WebPartManager 控件。 虽然从来都不可见，但此控件具有着协调页面上的所有 Web 部件控件的关键任务。 例如，它跟踪各个 Web 部件控件。 管理 Web 部件区域 （包含在页面上的 Web 部件控件的区域），以及具体控件的区域。 它还会跟踪并控制页面可中，浏览、 连接、 编辑或目录模式下，以及个性化设置更改应用到所有用户或单个用户使用的不同的显示模式。 最后，它将启动并跟踪 Web 部件控件之间的连接和通信。

UI 结构组件，第二个类型为该区域。 区域作为 Web 部件页上的布局管理器。 它们包含和组织一部分类 （部件控件） 中派生的控件并提供能够执行水平或垂直方向中的模块化的页面布局。 区域还为常见且一致的用户界面元素 （如页眉和页脚样式、 标题、 边框样式、 操作按钮等） 提供有关它们包含; 每个控件这些常见的元素称为控件的 chrome。 在不同的显示模式并使用不同的控件使用的区域的多个专用的类型。 下面的 Web 部件基本控件部分中介绍了区域的不同类型。

Web 部件用户界面控件，所有这些派生**一部分**类中，包含 Web 部件页上的主用户界面。 Web 部件控件集灵活，非独占选项中它为您提供用于创建部件的控件。 除了创建你自己的自定义 Web 部件控件，还可以使用现有的 ASP.NET 服务器控件、 用户控件或自定义服务器控件用作 Web 部件控件。 最常用于创建 Web 部件页的基本控件下一节所述。

## <a name="web-parts-essential-controls"></a>Web 部件基本控件

Web 部件控件集很广泛，但某些控件至关重要，因为它们所需的 Web 部件正常工作，或因为它们是最常用的 Web 部件页上的控件。 在开始使用 Web 部件，并创建基本的 Web 部件页，最好先熟悉以下表中所述的基本 Web 部件控件。

| **Web 部件控件** | **说明** |
| --- | --- |
| WebPartManager | 管理页面上的所有 Web 部件控件。 一个 （且只有一个） **WebPartManager**控件是所必需的每个 Web 部件页。 |
| CatalogZone | 包含 CatalogPart 控件。 此区域用于创建用户可以从中选择要添加到页面的控件的 Web 部件控件目录。 |
| EditorZone | 包含 EditorPart 控件。 使用此区域以使用户能够编辑和个性化设置页面上的 Web 部件控件。 |
| WebPartZone | 包含并提供用于构成一个页面的主要用户界面的 web 部件控件的总体布局。 每当您创建具有 Web 部件控件的网页时，请使用此区域。 页面可以包含一个或多个区域。 |
| ConnectionsZone | 包含连接控件，并提供一个用户界面，用于管理连接。 |
| Web 部件 (GenericWebPart) | 呈现主用户界面;大多数 Web 部件用户界面控件属于此类别。 对于最大的编程控制，可以创建自定义 Web 部件控件派生自基**WebPart**控件。 用作 Web 部件控件，还可以使用现有服务器控件、 用户控件或自定义控件。 任何这些控件放置在区域，每当**WebPartManager**控件自动换行与它们**GenericWebPart**控件在运行时，以便可以使用 Web 部件的功能。 |
| CatalogPart | 包含用户可添加到页面的可用 Web 部件控件的列表。 |
| WebPartConnection | 创建页面上的两个 Web 部件控件之间的连接。 连接定义了 （数据），提供，作为使用者将另一个 Web 部件控件。 |
| EditorPart | 用作专用的编辑器控件的基类。 |
| EditorPart 控件 （AppearanceEditorPart、 LayoutEditorPart、 BehaviorEditorPart 和 PropertyGridEditorPart） | 允许用户进行个性化设置页面上的 Web 部件用户界面控件的各个方面 |

## <a name="lab-create-a-web-part-page"></a>实验室： 创建 Web 部件页

在此实验中，将创建将保留通过 ASP.NET 配置文件信息的 Web 部件页。

### <a name="creating-a-simple-page-with-web-parts"></a>使用 Web 部件创建一个简单的页面

在本演练的此部分中，创建使用 Web 部件控件来显示静态内容的页面。 使用 Web 部件的第一步是创建具有两个所需的结构化元素的页。 首先，Web 部件页需要一个 WebPartManager 控件跟踪并协调所有 Web 部件控件。 第二，Web 部件页需要一个或多个区域，包含 web 部件或其他服务器控件和占用页面的指定的区域的复合控件。

> [!NOTE]
> 不需要执行任何操作即可启用 Web 部件个性化设置;对于 Web 部件控件集默认情况下启用它。 当你首次运行站点上的 Web 部件页时，ASP.NET 会设置默认个性化设置提供程序来存储用户的个性化设置。 个性化设置的详细信息，请参阅 Web 部件个性化设置概述。


### <a name="to-create-a-page-for-containing-web-parts-controls"></a>若要创建包含 Web 部件控件的页

1. 关闭默认页，将新页面添加到名为 WebPartsDemo.aspx 的站点。
2. 切换到**设计**视图。
3. 从**视图**菜单中，请确保**非可视控件**并**详细信息**选项处于选中状态，以便您可以看到布局标记和不具有用户界面的控件。
4. 将插入点之前`<div>`设计图面上，然后按 ENTER 以添加新行上的标记。 将光标移至新行字符之前，请单击**块格式**下拉列表控件的菜单上，并选择**标题 1**选项。 在标题中，添加文本**Web 部件演示页**。
5. 从**WebParts**选项卡的工具箱拖动**WebPartManager**控件拖到页上，只需在新行字符之后和之前将它`<div>`标记。   
  
   **WebPartManager**控件不呈现任何输出，使其显示为设计器图面上的灰色框。
6. 在将插入点位置`<div>`标记。
7. 在中**布局**菜单上，单击**插入表**，并创建具有一个行和三个列的新表。 单击**Cell Properties**按钮，选择**顶部**从**垂直对齐**下拉列表中，单击**确定**，然后单击**确定**再次以创建的表。
8. 将 WebPartZone 控件拖到左的表列。 右键单击**WebPartZone**控制中，选择**属性**，并设置以下属性：   
  
   ID: SidebarZone   
  
   HeaderText： 侧栏
9. 将另一个**WebPartZone**控制到中间的表列并设置以下属性：   
  
   ID: MainZone   
  
   HeaderText: Main
10. 保存该文件。

页面现在包含两个不同的区域，您可以单独控制。 但是，两个区域中包含任何内容，因此是下一步创建的内容。 在本演练中，使用仅显示静态内容的 Web 部件控件。

通过指定 Web 部件区域的布局&lt;方法&gt;元素。 在区域模板中，您可以添加任何 ASP.NET 控件，是否自定义 Web 部件控件、 一个用户控件或为现有服务器控件。 请注意，此处使用标签控件，并向，只需添加静态文本。 在将中的常规服务器控件**WebPartZone**区域，ASP.NET 将控件视为 Web 部件控件在运行时，可以实现在控件上的 Web 部件功能。

**若要创建主区域的内容**

1. 在中**设计**视图中，将**标签**控件从**标准**选项卡的工具箱拖动到该区域的内容区域其**ID**属性设置为 MainZone。
2. 切换到**源**视图。 请注意，&lt;方法&gt;已添加元素来包装**标签**MainZone 中的控件。
3. 添加名为的属性**标题**到&lt;asp: label&gt;元素，并将其值设置为内容。 删除文本 ="Label"属性从&lt;asp: label&gt;元素。 开始和结束标记之间&lt;asp: label&gt;元素中，添加一些文本，例如**欢迎来到我的主页**一对大&lt;h2&gt;元素标记。 你的代码应如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. 保存该文件。

接下来，创建用户控件，还可以添加到作为 Web 部件控件的页。

### <a name="to-create-a-user-control"></a>创建用户控件

1. 将新的 Web 用户控件添加到您的网站作为一个搜索控件。 取消选择选项**将源代码放在单独的文件**。 将其添加为 WebPartsDemo.aspx 页中，相同的目录中并将其命名 SearchUserControl.ascx。   
  
    > [!NOTE]
    > 在本演练中的用户控件不实现龟悔穓碝这样的功能。它仅用于说明 Web 部件的功能。
2. 切换到**设计**视图。 从**标准**选项卡的工具箱将 TextBox 控件拖到绘图页上。
3. 将插入点放在刚添加的文本框后，然后按 ENTER 以添加新行。
4. 将按钮控件拖到页上您刚添加的文本框下方的新行。
5. 切换到**源**视图。 请确保用户控件的源代码如下面的示例所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. 保存并关闭文件。

现在你可以将 Web 部件控件添加到侧栏区域。 要将两个控件添加到该侧栏区域，在前面过程中创建的一个包含列表的链接，另一个则是用户控制。 作为一种标准添加链接**标签**服务器控件，类似于创建主区域的静态文本的方式。 但是，尽管中包含的单个服务器控件可以直接在区域 （如标签控件） 中包含用户控件，它们在这种情况下不是。 相反，它们是在前面过程中创建的用户控件的一部分。 此示例演示包的任何控件和用户控件中所需的额外功能，然后引用该控件作为 Web 部件控件区域中的常用方法。

在运行时，Web 部件控件集包装 GenericWebPart 控件与这两个控件。 当**GenericWebPart**控件换行的 Web 服务器控件，泛型部件控件是父控件，可以通过父控件的 ChildControl 属性访问的服务器控件。 此泛型部件控件的使用使标准的 Web 服务器控件与派生的 Web 部件控件具有相同的基本行为和属性**WebPart**类。

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>若要将 Web 部件控件添加到侧栏区域

1. 打开 WebPartsDemo.aspx 页。
2. 切换到**设计**视图。
3. 将用户控件创建的页，SearchUserControl.ascx，从**解决方案资源管理器**入区其**ID**属性设置为 SidebarZone，并且存在删除。
4. 保存 WebPartsDemo.aspx 页。
5. 切换到**源**视图。
6. 内部&lt;asp: webpartzone&gt; SidebarZone，对你的用户控件的引用的正上方的元素添加&lt;asp: label&gt;具有元素包含的链接，如下面的示例中所示。 此外，添加**标题**属性为用户控件标记中，值为**搜索**，如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. 保存并关闭文件。

现在，你可以通过在浏览器中浏览到它测试您的页面。 该页将显示两个区域。 下面的屏幕截图显示的页。

**具有两个区域的 web 部件演示页**


![Web 部件 VS 演练 1 屏幕截图](profiles-themes-and-web-parts/_static/image3.gif)

**图 3**: Web 部件 VS 演练 1 屏幕截图


标题栏中的每个控件都提供了对可以在控件执行的可用操作的谓词菜单访问的向下箭头。 单击其中一个控件的谓词菜单，然后单击**最小化**谓词，会发现，最小化控件。 从谓词菜单中，单击**还原**，并控制返回到其正常大小。

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>使用户能够编辑页和更改布局

Web 部件提供了用户可以将它们从一个区域拖到另一个更改 Web 部件控件的布局的功能。 还允许用户继续**WebPart**控件到另一个区域，可以允许用户编辑控件，包括其外观、 布局和行为的各种特征。 Web 部件控件集提供的基本编辑功能**WebPart**控件。 尽管未将此，在本演练中，你可以创建允许用户编辑的功能的自定义编辑器控件**WebPart**控件。 与更改的位置一样**WebPart**控件，编辑控件的属性依赖于 ASP.NET 个性化设置，以保存用户所做的更改。

在本演练的此部分中，添加用户若要编辑的任何基本特征的能力**WebPart**页上的控件。 若要启用这些功能，您将添加另一个自定义用户控件到页上，连同&lt;asp: editorzone&gt;元素和两个编辑控件。

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>若要创建一个用户控件，可以更改页面布局

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建**子菜单，然后单击**文件**选项。
2. 在中**添加新项**对话框中，选择**Web 用户控件**。 将新文件 DisplayModeMenu.ascx 名称。 取消选择选项**将源代码放在单独的文件**。
3. 单击添加创建新的控件。
4. 切换到**源**视图。
5. 在新的文件中，删除所有现有的代码并粘贴以下代码中。 此用户控件代码使用支持页后，可以更改其视图或显示模式下，Web 部件控件集的功能，还可用于更改物理外观和布局时页面的特定显示模式中。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. 单击保存保存该文件图标的工具栏上，或通过选择**保存**上**文件**菜单。

### <a name="to-enable-users-to-change-the-layout"></a>若要使用户能够更改布局

1. 打开 WebPartsDemo.aspx 页上，并切换到**设计**视图。
2. 在将插入点放**设计**之后查看**WebPartManager**前面添加的控件。 文本之后添加硬回车，使后的空行**WebPartManager**控件。 将插入点放在空行上。
3. 将刚创建的用户控件 （该文件被命名为 DisplayModeMenu.ascx） 到 WebPartsDemo.aspx 页上，并将其放在空行上。
4. 中的 EditorZone 控件拖**web 部件**工具箱拖到 WebPartsDemo.aspx 页中的剩余打开表单元格部分。
5. 从**WebParts**部分的工具箱拖动 AppearanceEditorPart 控件和将 LayoutEditorPart 控件插入**EditorZone**控件。
6. 切换到**源**视图。 表单元格中生成的代码应类似于下面的代码。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. 保存 WebPartsDemo.aspx 文件。 已创建用户控件，您可以更改显示模式和更改页面布局，并引用主网页上的控件。

现在可以测试编辑页并更改布局的功能。

### <a name="to-test-layout-changes"></a>若要测试的布局更改

1. 在浏览器页面加载。
2. 单击**显示模式**下拉列表菜单，然后选择**编辑**。 区域标题显示。
3. 拖动**我的链接**通过它从侧栏区域到主要区域底部的标题栏控件。 您的页面应如以下屏幕截图所示。

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>与我的链接控件移动的 web 部件演示页


![Web 部件 VS 演练 2 屏幕截图](profiles-themes-and-web-parts/_static/image4.gif)

**图 4**: Web 部件 VS 演练 2 屏幕截图


1. 单击**显示模式**下拉列表菜单，然后选择**浏览**。 刷新页面，区域名称消失，并且**我的链接**控制的保持您放置的位置。
2. 若要演示的个性化设置正常工作，关闭浏览器，然后重新加载页面。 对于将来的浏览器会话保存所做的更改。
3. 从**显示模式**菜单中，选择**编辑**。   
  
   在页上的每个控件现在显示一个标题栏，其中包含谓词下拉列表菜单中的向下箭头。
4. 单击箭头以显示上的谓词菜单**我的链接**控件。 单击**编辑**谓词。   
  
   **EditorZone**控件将出现，显示 EditorPart 控制你添加。
5. 在**外观**部分中的编辑控件，更改**标题**到我的收藏夹，使用**部件版式类型**下拉列表选择**仅标题**，然后单击**应用**。 下面的屏幕截图显示页面处于编辑模式。

### <a name="web-parts-demo-page-in-edit-mode"></a>在编辑模式下的 web 部件演示页


![Web 部件 VS 演练 3 屏幕截图](profiles-themes-and-web-parts/_static/image5.gif)

**图 5**: Web 部件 VS 演练 3 屏幕截图


1. 单击**显示模式**菜单，然后选择**浏览**以返回到浏览模式。
2. 该控件现在具有更新后的标题和没有边框，如以下屏幕截图中所示。

### <a name="edited-web-parts-demo-page"></a>编辑的 Web 部件演示页


![Web 部件 VS 演练 4 屏幕截图](profiles-themes-and-web-parts/_static/image6.gif)

**图 4**: Web 部件 VS 演练 4 屏幕截图


### <a name="adding-web-parts-at-run-time"></a>在运行时添加 Web 部件

此外可以允许用户在运行时将 Web 部件控件添加到他们的页面。 若要执行此操作，请使用 Web 部件目录，其中包含你想要向用户提供的 Web 部件控件的列表配置页。

**若要允许用户在运行时添加 Web 部件**

1. 打开 WebPartsDemo.aspx 页上，并切换到**设计**视图。
2. 从**WebParts**选项卡的工具箱 CatalogZone 将控件拖到右侧的表的列下**EditorZone**控件。   
  
   因为它们不会显示在同一时间，这两个控件可以是相同的表单元中。
3. 在属性窗格中，将字符串分配**添加 Web 部件**HeaderText 属性**CatalogZone**控件。
4. 从**WebParts**部分的工具箱将 DeclarativeCatalogPart 控件拖动到的内容区域**CatalogZone**控件。
5. 单击右上角中的箭头**DeclarativeCatalogPart**控制公开其任务菜单，然后选择**编辑模板**。
6. 从**标准**部分中的工具箱拖动**FileUpload**控件和一个**日历**控制**WebPartsTemplate**部分**DeclarativeCatalogPart**控件。
7. 切换到**源**视图。 检查的源代码&lt;asp: catalogzone&gt;元素。 请注意， **DeclarativeCatalogPart**控件包含&lt;webpartstemplate&gt;具有两个包含的服务器控件，你将能够从目录中添加到您的页面元素。
8. 添加**标题**属性设置为每个控件添加到目录中，使用下面的代码示例中的每个标题显示的字符串值。 即使标题不是属性可以正常情况下设置这些这两个服务器控件在设计时，当用户添加到这些控件**WebPartZone**区域中在运行时目录，它们的每个包装与**GenericWebPart**控件。 这可让其充当 Web 部件控件，因此他们将能够显示的标题。   
  
   中包含的两个控件的代码**DeclarativeCatalogPart**控件的外观应按如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. 保存页。

现在可以测试目录。

### <a name="to-test-the-web-parts-catalog"></a>若要测试 Web 部件目录

1. 在浏览器页面加载。
2. 单击**显示模式**下拉列表菜单，然后选择**目录**。   
  
   标题为的目录**添加 Web 部件**显示。
3. 拖动**我的收藏夹**控制从主区域回复到顶部的侧栏区域中，并将其放在那里。
4. 在中**添加 Web 部件**目录，选择这两个复选框，并选择**Main**从包含在可用性区域的下拉列表。
5. 单击**添加**目录中。 这些控件添加到主区域中。 如果需要，可以将控件的多个实例从目录添加到您的页面。   
  
   下面的屏幕截图显示在主区域中有文件上传控件和日历的页。 

![控件从目录添加到主区域](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. 单击**显示模式**下拉列表菜单，然后选择**浏览**。 目录将消失，刷新页面。
7. 关闭浏览器。 重新加载页面。 您所做的更改持久保存。
