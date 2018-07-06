---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 创建 MVC 3 应用程序使用 Razor 和非介入式 JavaScript |Microsoft Docs
author: microsoft
description: 用户列表示例 web 应用程序演示如何创建使用 Razor 视图引擎的 ASP.NET MVC 3 应用程序是多么简单。 示例应用程序 s...
ms.author: aspnetcontent
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: 136c87cba70525da53c1f74576c50c12f8759539
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840457"
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>创建 MVC 3 应用程序使用 Razor 和非介入式 JavaScript
====================
by [Microsoft](https://github.com/microsoft)

> 用户列表示例 web 应用程序演示如何创建使用 Razor 视图引擎的 ASP.NET MVC 3 应用程序是多么简单。 示例应用程序演示如何使用 ASP.NET mvc 版本 3 的新 Razor 视图引擎和 Visual Studio 2010 创建一个虚构的用户列表网站，包括功能，例如创建、 显示、 编辑和删除用户。
> 
> 本教程介绍为了构建用户列表示例 ASP.NET MVC 3 应用程序已执行的步骤。 包含 C# 和 VB 源代码的 Visual Studio 项目是可随附于本主题：[下载](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。 如果您有关于本教程的问题，请将其发布到[MVC 论坛](https://forums.asp.net/1146.aspx)。


## <a name="overview"></a>概述

你将构建的应用程序是一个简单的用户列表网站。 用户可以输入、 查看和更新用户信息。

![示例站点](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

您可以下载 VB 和 C# 已完成的项目[此处](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)。

## <a name="creating-the-web-application"></a>创建 Web 应用程序

若要开始本教程，请打开 Visual Studio 2010 并创建新项目使用*ASP.NET MVC 3 Web 应用程序*模板。 该应用程序命名&quot;Mvc3Razor&quot;。

[![新的 MVC 3 项目](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**，选择 Razor 视图引擎，，然后单击**确定**。

![新建 ASP.NET MVC 3 项目对话框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

在本教程中你将不使用 ASP.NET 成员资格提供程序，因此可以删除与登录名和成员身份相关联的所有文件。 在中**解决方案资源管理器**，删除以下文件和目录：

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* （和此目录中的所有文件）

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

编辑 <em>\_Layout.cshtml</em>文件，然后替换中的标记`<div>`名为元素`logindisplay`并显示消息 <em>&quot;</em>登录名已禁用&quot;. 下面的示例显示了新的标记：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>添加模型

在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后单击**类**。

![新用户 Mdl 类](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

将此类命名为 `UserModel`。 内容替换为*UserModel*文件使用以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel`类表示的用户。 类的每个成员添加批注[所需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性从[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间。 中的属性[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供的 web 应用程序的自动客户端和服务器端验证。

打开`HomeController`类，并添加`using`指令，以便可以访问`UserModel`和`Users`类：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

后面`HomeController`声明中，添加下面的注释以及对引用`Users`类：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users`类是将在本教程中使用的简化的内存中数据存储。 在实际的应用程序将使用数据库来存储用户信息。 前的几行`HomeController`文件显示在下面的示例：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

生成应用程序，以便用户模型将可供下一步中的基架向导。

## <a name="creating-the-default-view"></a>创建的默认视图

下一步是添加一个操作方法和视图以显示用户。

删除现有*Views\Home\Index*文件。 您将创建一个新*索引*文件以显示用户。

在中`HomeController`类中的内容替换为`Index`方法使用以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

内右击`Index`方法，然后单击**添加视图**。

![添加视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

选择**创建强类型化视图**选项。 有关**查看数据类**，选择**Mvc3Razor.Models.UserModel**。 (如果看不到**Mvc3Razor.Models.UserModel**中**查看数据类**框中，您需要生成项目。)请确保视图引擎设置为**Razor**。 设置**查看内容**到**列表**，然后单击**添加**。

![添加索引视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新视图自动搭建基架以传递给的用户数据`Index`视图。 检查新生成*Views\Home\Index*文件。 **创建新**，**编辑**，**详细信息**，以及**删除**链接不起作用，但页的其余部分将正常运行。 运行页。 请参阅用户的列表。

![索引页](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

打开*Index.cshtml*文件，然后替换`ActionLink`标记**编辑**，**详细信息**，并**删除**用下面的代码:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

用户名称用作 ID 查找中的所选的记录**编辑**，**详细信息**，并**删除**链接。

## <a name="creating-the-details-view"></a>创建详细信息视图

下一步是添加`Details`操作方法和视图以显示用户详细信息。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

以下代码添加到`Details`向主控制器的方法：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

内右击`Details`方法，然后选择<strong>添加视图</strong>。 确认<strong>查看数据类</strong>框中包含<strong>Mvc3Razor.Models.UserModel</strong><em>。</em> 设置<strong>查看内容</strong>到<strong>详细信息</strong>，然后单击<strong>添加</strong>。

![添加详细信息视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

运行应用程序并选择详细信息链接。 自动基架显示模型中的每个属性。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>创建编辑视图

以下代码添加到`Edit`向主控制器的方法。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

添加一个视图，如下所示的上一步骤，但设置**查看内容**到**编辑**。

![添加编辑视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

运行应用程序和编辑的一个用户的第一个和最后一个名称。 如果您违反`DataAnnotation`已应用于的约束`UserModel`类，当您提交窗体中，您将看到所生成的服务器代码的验证错误。 例如，如果您更改名字&quot;Ann&quot;到&quot;A&quot;，当您提交窗体中，在窗体上显示以下错误：

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

在本教程中，要将用户名称，视为主键。 因此，无法更改用户名属性。 在中*Edit.cshtml*文件，之后`Html.BeginForm`语句中，设置要隐藏的字段的用户名称。 这会导致要在模型中传递的属性。 以下代码片段演示的放置`Hidden`语句：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

替换`TextBoxFor`并`ValidationMessageFor`标记的用户名称和`DisplayFor`调用。 `DisplayFor`方法显示的属性为只读的元素。 下面的示例显示了完成的标记。 原始`TextBoxFor`并`ValidationMessageFor`调用注释掉使用 Razor 注释开始和结束注释字符 (`@* *@`)

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>启用客户端验证

若要在 ASP.NET MVC 3 中的客户端验证，必须设置两个标记，并且必须包含三个 JavaScript 文件。

打开应用程序的*Web.config*文件。 验证是否`that ClientValidationEnabled`和`UnobtrusiveJavaScriptEnabled`设置为 true 的应用程序设置。 以下片段中根*Web.config*文件显示了正确的设置：

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

设置`UnobtrusiveJavaScriptEnabled`为 true 启用非介入式 Ajax 和非介入式客户端验证。 当您使用非介入式验证时，验证规则转变成 HTML5 属性。 HTML5 属性名称可以包含小写字母、 数字和短划线。

设置`ClientValidationEnabled`为 true，则启用客户端验证。 通过在应用程序中设置这些密钥*Web.config*文件中，启用客户端验证和整个应用程序的非介入式 JavaScript。 您还可以启用或禁用这些设置在单个视图中或在控制器方法中使用以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

此外需要在呈现的视图中包含多个 JavaScript 文件。 若要在所有视图中包括 JavaScript 的简单方法是将其添加到*views/shared\\_Layout.cshtml*文件。 替换`<head>`的元素 *\_Layout.cshtml*文件使用以下代码：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

前两个 jQuery 脚本托管的 Microsoft Ajax 内容交付网络 (CDN)。 通过利用 Microsoft Ajax CDN，可以显著提高你的应用程序的第一个命中性能。

运行应用程序，并单击编辑链接。 在浏览器中查看页面的源。 浏览器源将显示在窗体的多个属性`data-val`（用于数据验证）。 当启用了客户端验证和非介入式 JavaScript 时，与客户端验证规则的输入的字段包含`data-val="true"`属性触发非介入式客户端验证。 例如，`City`模型中的字段使用修饰[所需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性，这会导致以下示例所示的 HTML:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

对于每个客户端验证规则，将添加属性，其形式`data-val-rulename="message"`。 使用`City`更早版本，显示所需的客户端验证规则将生成的字段示例`data-val-required`属性和消息&quot;City 字段是必填&quot;。 运行应用程序，编辑一个用户，并清除`City`字段。 当您 tab 键跳出字段时，您将看到客户端验证错误消息。

![所需的城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同样，对于客户端验证规则中每个参数，将添加属性，其形式`data-val-rulename-paramname=paramvalue`。 例如，`FirstName`属性将批注[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性，并指定 3 的最小长度和最大长度为 8。 名为的数据验证规则`length`具有参数的名称`max`和参数值 8。 下面的示例演示为生成的 HTML`FirstName`字段的一个用户编辑时：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

有关非介入式客户端验证的详细信息，请参阅文章[在 ASP.NET MVC 3 中的非介入式客户端验证](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)Brad Wilson 的博客中。

> [!NOTE]
> 在 ASP.NET MVC 3 Beta，有时需要提交窗体，以便启动客户端验证。 这可能会更改的最终版本。


## <a name="creating-the-create-view"></a>创建创建视图

下一步是添加`Create`操作方法和视图以使用户能够创建新的用户。 以下代码添加到`Create`向主控制器的方法：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

添加一个视图，如下所示的上一步骤，但设置**查看内容**到**创建**。

![创建视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

运行应用程序中，选择**创建**链接，并添加新用户。 `Create`方法自动利用的客户端和服务器端验证。 尝试输入的用户名称，包含空格，如&quot;Ben X&quot;。 当带用户名称字段中，客户端验证错误选项卡 (`White space is not allowed`) 显示。

## <a name="add-the-delete-method"></a>添加 Delete 方法

若要完成本教程，添加以下`Delete`向主控制器的方法：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

添加`Delete`视图，如前面的步骤，设置中所示**查看内容**到**删除**。

![删除视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

现可简单但功能完备的 ASP.NET MVC 3 应用程序，进行验证。
