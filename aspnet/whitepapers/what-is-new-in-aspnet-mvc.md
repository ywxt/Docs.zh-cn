---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: 什么是 ASP.NET MVC 2 中的新增功能 |Microsoft Docs
author: rick-anderson
description: 本文档介绍新功能和改进在 ASP.NET MVC 2 中引入的。 本文档也是可供下载。
ms.author: aspnetcontent
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: 54f62b0f6bbde50f53d062eda422f5f58806cbe1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834159"
---
<a name="whats-new-in-aspnet-mvc-2"></a>什么是 ASP.NET MVC 2 中的新增功能
====================
> 本文档介绍新功能和改进在 ASP.NET MVC 2 中引入的。 本文档也是可用于[下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)


[简介](#_TOC1)   
[将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2](#_TOC2)   
[新增功能](#_TOC3)   
[模板化帮助器](#_TOC3_1)   
[区域](#_TOC3_2)   
[对异步控制器的支持](#_TOC3_3)   
[DefaultValueAttribute 在操作方法参数的支持](#_TOC3_4)   
[对二进制数据使用模型绑定器绑定的支持](#_TOC3_5)   
[所对应的 ModelMetadata 和 ModelMetadataProvider 类](#_TOC3_6)   
[DataAnnotations 特性的支持](#_TOC3_7)   
[模型验证程序提供程序](#_TOC3_8)   
[客户端验证](#_TOC3_9)   
[Visual Studio 2010 的新代码段](#_TOC3_10)   
[新 RequireHttpsAttribute 操作筛选器](#_TOC3_11)   
[重写的 HTTP 方法谓词](#_TOC3_12)   
[用于模板化帮助器的新 HiddenInputAttribute 类](#_TOC3_13)   
[Html.ValidationSummary 帮助器方法可显示模型级错误](#_TOC3_14)   
[T4 模板在 Visual Studio 生成的代码特定于到目标版本的.NET framework](#_TOC3_15)[API 改进](#_TOC4)  
[重大更改](#_TOC5)  
[免责声明](#_TOC6)  

## <a id="_TOC1"></a>  简介

ASP.NET MVC 2 基于 ASP.NET MVC 1.0，而引入了大量的增强功能和侧重于提高工作效率的功能。 此版本是与 ASP.NET MVC 1.0 兼容，因此所有知识、 技能、 代码和扩展的 ASP.NET MVC 1.0 都继续应用。

有关 ASP.NET MVC 的详细信息，请访问以下资源：

- [MSDN 上的 ASP.NET MVC 文档](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC 网站](https://asp.net/mvc/)
- [ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)

## <a id="_TOC2"></a>  将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2

使应用程序开发人员灵活地选择何时升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序在同一服务器上，可以与 ASP.NET MVC 1.0 并行安装 ASP.NET MVC 2。 有关如何升级的信息，请参阅文档[升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序](https://go.microsoft.com/fwlink/?LinkID=185459)。

## <a id="_TOC3"></a>  新增功能

本部分介绍已引入的功能在 MVC 2 版本。

### <a id="_TOC3_1"></a>  模板化帮助器

模板化帮助器可自动关联的 HTML 元素以进行编辑和显示数据类型。 例如，当在视图中显示 System.DateTime 类型的数据时，日期选取器 UI 元素可以自动呈现。 这是类似于字段模板在 ASP.NET 动态数据中的工作方式。 有关详细信息，请参阅[显示的数据使用模板化帮助器](https://go.microsoft.com/fwlink/?LinkId=159062)MSDN 网站上。

### <a id="_TOC3_2"></a>  区域

区域中，可以将大型项目组织到多个较小部分，为了管理复杂性的大型 Web 应用程序。 每个部分 （"区域"） 通常表示大型网站的单独部分，并用于分组相关的控制器和视图集。 有关详细信息，请参阅[演练： 组织 ASP.NET MVC 应用程序按区域](https://go.microsoft.com/fwlink/?LinkId=158978)MSDN 网站上。

若要创建新区域中，在解决方案资源管理器中，右键单击项目，单击添加，然后单击区域。 这将显示一个对话框，提示你输入区域名称。 输入区域名称后，Visual Studio 向项目添加一个新的区域。

下图显示了具有两个方面，管理员和博客的项目布局示例。

![](what-is-new-in-aspnet-mvc/_static/image1.png)

在创建区域时，Visual Studio 将添加到每个区域从 AreaRegistration 派生的类。 此类所需注册的区域和其路由中，如下面的示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2 的默认项目模板在 Global.asax 文件的代码中包括对 RegisterAllAreas 方法的调用。 此方法查找从 AreaRegistration 类派生的所有类型、 实例化类型的实例并在实例上调用了 RegisterArea 方法，通过在项目中注册每个区域。 下面的示例演示如何做到这一点。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

如果你不要通过调用上下文中了 RegisterArea 方法，指定命名空间。默认情况下使用 Namespaces.Add 方法，注册类的命名空间。

### <a id="_TOC3_3"></a>  对异步控制器的支持

ASP.NET MVC 2 现在允许控制器来异步处理请求。 这可能会导致性能提升允许服务器在其中经常调用 （例如网络请求） 的阻塞操作改为调用非阻止对应项。 有关详细信息，请参阅[ASP.NET MVC 中使用异步控制器](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx)MSDN 上的主题。

### <a id="_TOC3_4"></a>  DefaultValueAttribute 在操作方法参数的支持

System.ComponentModel.DefaultValueAttribute 类允许要提供有关操作方法的自变量参数的默认值。 例如，假设以下默认路由的定义：

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

此外假设以下控制器和操作方法的定义：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

以下请求的任何 Url 将调用在前面的示例中定义的视图操作方法。

- / 文章/视图/123
- / 文章/视图/123？ 页 = 1 （有效地与相同上一个请求）
- / 文章/视图/123？ 页 = 2

如果不使用 DefaultValueAttribute 属性中，前面的列表中的第一个 URL 可不使用，因为页参数为非 null 的值类型尚未提供其值。

如果你的代码在 Visual Basic 2010 或 Visual C# 2010年中编写的您可以而不是 DefaultValueAttribute 属性中，使用可选参数，如下面的示例中所示：

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a id="_TOC3_5"></a>  对二进制数据使用模型绑定器绑定的支持

有两个新重载 Html.Hidden 帮助程序进行编码以 base-64 编码字符串形式的二进制值：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

一种典型用法是将在视图中嵌入对象时的时间戳。 例如，你的应用程序可能包括以下产品对象：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

编辑窗体可以呈现形式如下面的示例中所示的时间戳属性：

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

此标记将使用时间戳值隐藏的 input 的元素呈现为 base-64 编码的字符串，类似于下面的示例：

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

此窗体可能会发布到具有产品类型的自变量的操作方法，如下面的示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

在操作方法中，因为已发布的 base-64 编码字符串转换为字节数组正确填充时间戳属性。

### <a id="_TOC3_6"></a>  所对应的 ModelMetadata 和 ModelMetadataProvider 类

ModelMetadataProvider 类提供了用于获取视图内模型的元数据的抽象。 MVC 2 包括默认的提供程序，它提供通过 System.ComponentModel.DataAnnotations 命名空间中的属性公开的元数据。 就可以创建提供从其他数据存储，如数据库或 XML 文件的元数据的元数据提供程序。

ViewDataDictionary 该类会公开所对应的 ModelMetadata 对象，其中包含由 ModelMetadataProvider 类从模型中提取的元数据。 这样，若要使用此元数据，并相应地调整其输出的模板化帮助器。

有关详细信息，请参阅的文档[所对应的 ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx)并[ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx)类。

### <a id="_TOC3_7"></a>  DataAnnotations 特性的支持

ASP.NET MVC 2 支持使用 RangeAttribute、 RequiredAttribute、 StringLengthAttribute 和 RegexAttribute 验证特性 （System.ComponentModel.DataAnnotations 命名空间中定义） 时向模型绑定以提供输入验证。

有关详细信息，请参阅[如何： 验证模型数据使用 DataAnnotations 特性](https://go.microsoft.com/fwlink/?LinkId=159063)MSDN 网站上。 演示如何使用这些属性的示例项目是可在下载[ https://go.microsoft.com/fwlink/?LinkId=157753 ](https://go.microsoft.com/fwlink/?LinkId=157753)。

### <a id="_TOC3_8"></a>  模型验证程序提供程序

模型验证提供程序类表示为模型提供验证逻辑的抽象。 ASP.NET MVC 包括基于 System.ComponentModel.DataAnnotations 命名空间中包含的验证属性的默认提供程序。 此外可以创建自己的验证提供程序定义自定义验证规则和验证规则的自定义映射到模型。 有关详细信息，请参阅的文档[ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx)类。

### <a id="_TOC3_9"></a>  客户端验证

模型验证程序提供程序类公开为可由客户端验证库使用的 JSON 序列化数据的窗体中的浏览器验证元数据。 ASP.NET MVC 2 包括客户端验证库和支持 DataAnnotations 命名空间验证特性前面所述的适配器。 提供程序类还可以通过编写适配器，用于处理 JSON 数据并调用到备用的库使用其他客户端验证库。

### <a id="_TOC3_10"></a>  Visual Studio 2010 的新代码段

使用 Visual Studio 2010 安装 ASP.NET MVC 2 的 HTML 代码段的一组。 若要在工具菜单中查看这些代码段的列表，请选择代码片段管理器。 对于语言，选择 HTML，并对于位置，选择 ASP.NET MVC 2。 有关如何使用代码片段的详细信息，请参阅 Visual Studio 文档。

### <a id="_TOC3_11"></a>  新 RequireHttpsAttribute 操作筛选器

ASP.NET MVC 2 包括一个新的 RequireHttpsAttribute 类，可以应用于操作方法和控制器。 默认情况下，筛选器将非 SSL HTTP 请求重定向到已启用 SSL (HTTPS) 等效项。

### <a id="_TOC3_12"></a>  重写的 HTTP 方法谓词

通过使用 REST 体系结构风格生成网站时，使用 HTTP 谓词来确定要对资源执行的操作。 REST 需要该应用程序支持各种常见的 HTTP 谓词，其中包括 GET、 PUT、 POST 和 DELETE。

ASP.NET MVC 2 包括可以应用于操作方法和该功能简洁的语法的新属性。 这些属性使 ASP.NET MVC 能够选择基于 HTTP 谓词的操作方法。 在以下示例中，POST 请求将调用第一个操作方法和 PUT 请求将调用第二个操作方法。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

在早期版本的 ASP.NET MVC 中，这些操作所需方法更详细的语法，如下面的示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

浏览器支持仅的 GET 和 POST HTTP 谓词，因为它不能发布到需要不同的谓词的操作。 因此不能以本机方式支持 RESTful 的所有请求。

但是，以支持基于 Rest 请求在 POST 期间，ASP.NET MVC 2 中引入新 HttpMethodOverride HTML 帮助器方法。 此方法将呈现隐藏的 input 的元素使窗体来有效地模拟任何 HTTP 方法。 例如，通过使用 HttpMethodOverride HTML 帮助器方法，你可以显示的窗体提交是 PUT 或 DELETE 请求。 HttpMethodOverride 的行为会影响以下属性：

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

隐藏的 input 的元素具有 X HTTP 的方法重写其名称和其值设置为 HTTP 谓词来模拟。 替代值可以还指定 HTTP 标头中或在查询字符串值作为名称/值对。

实际请求是 POST 请求时，可以仅使用重写。 使用任何其他 HTTP 谓词的请求将被忽略的覆盖值。

### <a id="_TOC3_13"></a>  用于模板化帮助器的新 HiddenInputAttribute 类

您可以将新的 HiddenInputAttribute 特性应用于模型属性以指示编辑器模板中显示该模型时是否应呈现隐藏的 input 的元素。 （该属性设置 HiddenInput 隐式 UIHint 值）。 特性的 DisplayValue 属性可以指定是否在编辑器中显示值和显示模式。 当 DisplayValue 设置为 false 时，将不会显示，即使通常围绕一个字段的 HTML 标记。 DisplayValue 的默认值为 true。

你可以在以下方案中使用 HiddenInputAttribute 属性：

- 当视图允许用户编辑的对象 ID 和需要显示的值也提供隐藏的 input 的元素，包括旧的 ID，使其可传递到控制器。
- 视图可让用户编辑应永远不会显示，例如时间戳属性的二进制属性。 在这种情况下，不显示的值和周围的 HTML 标记 （如标签和值）。

下面的示例演示如何使用 HiddenInputAttribute 类。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

当属性设置为 true （或未指定任何参数），将发生以下情况：

- 在显示模板中，标签将呈现在并向用户显示值。
- 编辑器模板中呈现一个标签和值呈现中隐藏的 input 元素。

如果该属性设置为 false，将发生以下情况：

- 显示模板中执行任何操作将呈现为该字段。
- 编辑器模板中呈现没有标签和值呈现中隐藏的 input 元素。

### <a id="_TOC3_14"></a>  Html.ValidationSummary 帮助器方法可显示模型级错误

而不是始终显示所有验证错误，Html.ValidationSummary 帮助器方法具有一个新选项以仅显示模型级错误。 这样，要在验证摘要中显示的模型级错误和特定于字段的每个字段旁边显示错误。

### <a id="_TOC3_15"></a>  在 Visual Studio 生成的代码特定于 T4 模板到.NET framework 目标版本

一个新的属性是可用 T4 文件从指定的应用程序使用.NET Framework 版本的 ASP.NET MVC T4 主机。 这使 T4 模板生成代码和特定于版本的.NET Framework 的标记。 在 Visual Studio 2008 中，值始终为.NET 3.5。 在 Visual Studio 2010 中，值为.NET 3.5 或.NET 4。

## <a id="_TOC4"></a>  API 改进

本部分介绍对现有的 ASP.NET MVC 类型和成员的更改。

- 在控制器类中添加了一个受保护的虚拟 CreateActionInvoker 方法。 此方法调用由控制器的 ActionInvoker 属性，如果已不设置任何调用程序用于调用程序的延迟实例化。
- AuthorizeAttribute 类中添加了一个受保护的虚拟 HandleUnauthorizedRequest 方法。 这使从 AuthorizeAttribute 授权失败时控制的行为派生的筛选器。
- ValueProviderDictionary 类中添加一个 Add （字符串、 对象键值） 方法。 这使您为 ValueProviderDictionary，使用字典初始值设定项语法，如以下示例所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- 添加 get\_对象 Sys.Mvc.AjaxContext 类中的方法。 这是一个 JavaScript 方法类似于 get\_数据的方法，但是如果响应的内容类型为 application/json，获取\_对象返回的 JSON 对象。
- AuthorizationContext 类中添加一个 ActionDescriptor 属性。
- 添加可用于绑定到属性时不存在包含 ID 属性的模型时解决问题的 UrlParameter.Optional 令牌表单发布中。 更多详细信息，请参阅文章[ASP.NET MVC 2 可选 URL 参数](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx)Phil Haack 的博客上。

## <a id="_TOC5"></a>  重大更改

以下更改可能导致现有 ASP.NET MVC 1.0 应用程序中出现错误。

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>实现 IDataErrorInfo 的类的属性验证行为更改

对于使用 IDataErrorInfo 来执行验证的模型对象，每个验证属性，而不考虑是否已设置新值。 在 ASP.NET MVC 1.0 中，已验证了设置的新值的属性。 在 ASP.NET MVC 2 中，仅当所有属性验证程序都已成功调用 IDataErrorInfo 的错误属性。

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>IIS 脚本映射脚本不再在安装程序中可用

IIS 脚本映射脚本是用于在经典模式下为 IIS 6 和 IIS 7 配置脚本映射的命令行脚本。 如果使用 Visual Studio 开发服务器，或在集成模式下使用 IIS 7，则不需要脚本映射脚本。 作为单独的不受支持下载上提供了脚本[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)。

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>Html.Substitute 帮助器方法在 MVC Futures 中的不再可用

由于 MVC 视图引擎的呈现行为发生变化，Html.Substitute 帮助器方法不起作用，并已删除。

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider 界面替代了 IDictionary 的所有用法

现在接受 IDictionary MVC 1.0 中的每个属性或方法参数接受 IValueProvider。 此更改仅影响应用程序，包括自定义值提供程序或自定义模型联编程序。 此更改影响的属性和方法的示例包括：

- ValueProvider ControllerBase 和 ModelBindingContext 类的属性。
- 控制器类 TryUpdateModel 方法。

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Site.css 文件中添加新的 CSS 类

已更新的 Site.css 文件中的 ASP.NET MVC 项目模板以包括新的验证功能和模板化帮助器所使用的样式。

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>帮助程序现在返回 MvcHtmlString 对象

若要充分利用新的 HTML 编码表达式语法的 ASP.NET 4 中，HTML 帮助程序的返回类型是现在 MvcHtmlString 而不是一个字符串。 如果在 ASP.NET 3.5 上使用 ASP.NET MVC 2 和新的帮助器，您将不能充分利用 HTML 编码语法;仅当您在 ASP.NET 4 上运行 ASP.NET MVC 2 时，新的语法是可用。

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult 现在只响应 HTTP POST 请求

为了缓解 JSON 劫持攻击，默认情况下，任何信息泄露的可能性 JsonResult 类现在仅响应 HTTP POST 请求。 应更改获取 Ajax 调用的操作方法的返回 JsonResult 对象，以改为使用 POST。 如有必要，您可以通过设置新的 JsonResult JsonRequestBehavior 属性重写此行为。 有关可能的攻击的详细信息，请参阅博客文章[JSON 劫持](http://haacked.com/archive/2009/06/25/json-hijacking.aspx)Phil Haack 的博客上。

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>模型和 ModelType 属性 setter ModelBindingContext 上的已过时

新的可设置所对应的 ModelMetadata 属性已添加到 ModelBindingContext 类。 新属性封装模型和 ModelType 属性。 尽管模型和 ModelType 属性已过时，但对于向后兼容性属性 getter 仍然可用;它们委托给所对应的 ModelMetadata 属性检索值。

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>借助于 DefaultControllerFactory 类更改会中断从其派生的自定义控制器工厂

通过删除 RequestContext 属性解决。 借助于 DefaultControllerFactory 类。 此属性，代替请求上下文实例传递到受保护的虚拟 GetControllerInstance 和 GetControllerType 方法。 此更改会影响从 DefaultControllerFactory 派生的自定义控制器工厂。

自定义控制器工厂通常用于提供应用程序的 ASP.NET MVC 的依赖关系注入。 若要更新以支持 ASP.NET MVC 2 的自定义控制器工厂，请更改方法签名或签名以匹配新的签名，并使用而不是属性的请求上下文参数。

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"区域"是保留的路由值键的现在

中的路由值的字符串"区域"现在在 ASP.NET MVC 中，具有特殊含义，"控制器"和"操作"执行操作的方式相同。 一个含义是，如果使用包含"区域"的路由值字典提供了 HTML 帮助程序，帮助程序将无法再追加"区域"查询字符串中。

如果使用 Areas 功能，请务必使用 {区域} 作为路由 URL 的一部分。


## <a id="_TOC6"></a>  免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。

© 2010 Microsoft Corporation. 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。
