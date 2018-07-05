---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (共 2 个 10) 中实现基本的 CRUD 功能与实体框架 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 7535a72afaa79260303e3094cbaf97f97132c1d5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399255"
---
<a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>在 ASP.NET MVC 应用程序 (共 2 个 10) 中实现基本的 CRUD 功能与实体框架
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


上一教程中创建的存储和显示数据使用实体框架和 SQL Server LocalDB 的 MVC 应用程序。 在本教程中将评审和自定义 CRUD （创建、 读取、 更新、 删除） 的 MVC 基架自动为你创建在控制器和视图中的代码。

> [!NOTE]
> 为了在控制器和数据访问层之间创建一个抽象层，常见的做法是实现存储库模式。 若要保持这些教程内容简单，不会之前在本系列后面的教程实现存储库。


在本教程中，你将创建以下网页：

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>创建详细信息页

面向学生的基架的代码`Index`页上留出`Enrollments`属性，因为该属性包含一个集合。 在`Details`页面将 HTML 表中显示集合的内容。

 在中*Controllers\StudentController.cs*，为操作方法`Details`查看使用`Find`方法来检索单个`Student`实体。 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 密钥的值传递给方法作为`id`参数和来自路由数据中**详细信息**索引页上的超链接。 

1. 打开*Views\Student\Details.cshtml*。 使用显示每个字段`DisplayFor`帮助程序，如下面的示例中所示： 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. 之后`EnrollmentDate`字段，然后立即在关闭前`fieldset`标记中，添加代码以显示注册，列表，如下面的示例中所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    此代码循环通过 `Enrollments` 导航属性中的实体。 每个`Enrollment`实体在属性中，它将显示课程标题和成绩。 课程标题检索从`Course`中存储的实体`Course`导航属性`Enrollments`实体。 所有这些数据是从数据库中检索自动在需要时。 （即，使用延迟加载此处。 未指定*预先加载*为`Courses`导航属性，使您尝试访问该属性第一次，查询发送到数据库以检索数据。 你可以阅读更多有关延迟加载和预先加载在[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列后面的教程。)
3. 通过选择运行页**学生**选项卡并单击**详细信息**Alexander Carson 的链接。 将看到所选学生的课程和年级列表：

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>正在更新创建页

1. 中*Controllers\StudentController.cs*，替换`HttpPost``Create`使用以下代码添加操作方法`try-catch`块并[绑定属性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)到基架生成的方法： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    此代码将添加`Student`ASP.NET MVC 模型绑定器创建实体到`Students`实体设置，并将所做的更改保存到数据库。 (*模型联编程序*指的是 ASP.NET MVC 功能，使其更轻松地处理提交的窗体的数据; 模型联编程序将发布窗体到 CLR 类型值，并将其传递给操作方法的参数。 这种情况下，模型绑定器实例化`Student`实体为你使用属性值从`Form`集合。)

    `ValidateAntiForgeryToken`特性帮助抵御[跨站点请求伪造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻击。

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.chstml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. 通过选择运行页**学生**选项卡并单击**创建新**。

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    默认情况下，一些数据验证工作原理。 输入名称和无效的日期，然后单击**创建**可查看错误消息。

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    以下突出显示的代码显示了模型验证检查。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    更改为有效的值如 2005 年 9 月 1 日的日期，然后单击**创建**若要查看中显示的新学生**索引**页。

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>更新编辑文章页面

在中*Controllers\StudentController.cs*，则`HttpGet``Edit`方法 (而不是`HttpPost`属性) 使用`Find`方法来检索所选`Student`作为您了解到实体，在`Details`方法。 不需要更改此方法。

但是，替换`HttpPost``Edit`使用以下代码添加操作方法`try-catch`块并[绑定属性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx):

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

此代码是类似于您在中看到`HttpPost``Create`方法。 但是，而不是添加到实体集的模型联编程序创建的实体，此代码指示已更改的实体上设置的标志。 当[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)调用方法时， [Modified](https://msdn.microsoft.com/library/system.data.entitystate.aspx)标志会导致实体框架来创建 SQL 语句来更新数据库行。 将更新数据库行中的所有列，包括用户未更改，并忽略并发冲突。 （您将了解如何在更高版本中本系列教程中处理的并发性）。

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>实体状态的附加和 SaveChanges 方法

数据库上下文跟踪内存中的实体是否与数据库中相应的行同步，并且此信息确定调用 `SaveChanges` 方法时会发生的情况。 例如，当传递到新的实体[外](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)方法，该实体的状态设置为`Added`。 然后调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法，将数据库上下文发出 SQL`INSERT`命令。

实体可能之一[遵循状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx):

- `Added`。 实体在数据库中尚不存在。 `SaveChanges`方法必须发出`INSERT`语句。
- `Unchanged`。 不需要通过 `SaveChanges` 方法对此实体执行操作。 从数据库读取实体时，实体将从此状态开始。
- `Modified`。 已修改实体的部分或全部属性值。 `SaveChanges`方法必须发出`UPDATE`语句。
- `Deleted`。 已标记该实体进行删除。 `SaveChanges`方法必须发出`DELETE`语句。
- `Detached`。 数据库上下文未跟踪该实体。

在桌面应用程序中，通常会自动设置状态更改。 在桌面应用程序的类型中，读取一个实体并对它的一些属性值进行更改。 这将使其实体状态自动更改为 `Modified`。 然后调用`SaveChanges`，Entity Framework 生成 SQL`UPDATE`更新仅更改了的实际属性的语句。

Web 应用断开连接的特性不允许此连续序列。 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)读取实体将在页面呈现后进行处理。 当`HttpPost``Edit`调用操作方法，将进行新的请求并具有的新实例[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)，因此您必须手动将实体状态设置为`Modified.`然后当您调用`SaveChanges`，Entity Framework 会更新所有列的数据库行，因为上下文无法知道已更改的属性。

如果您希望 SQL`Update`语句来更新字段的用户实际更改，您可以以某种方式 （如隐藏字段） 保存的原始值，以便它们时，将用`HttpPost``Edit`调用方法。 然后可以创建`Student`实体使用的原始值，调用`Attach`方法与该原始版本的实体的实体的值更新为新值，然后调用`SaveChanges.`的详细信息，请参阅[实体状态和 SaveChanges](https://msdn.microsoft.com/data/jj592676)并[本地数据](https://msdn.microsoft.com/data/jj592872)MSDN 数据开发人员中心中。

中的代码*Views\Student\Edit.cshtml*类似于您在中看到*Create.cshtml*，并不不需要任何更改。

通过选择运行页**学生**选项卡，然后单击**编辑**超链接。

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

更改某些数据并单击“保存”。 请参阅索引页中更改的数据。

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>正在更新删除页

在中*Controllers\StudentController.cs*的模板代码`HttpGet``Delete`方法使用`Find`方法来检索所选`Student`实体，为你在中看到`Details`和`Edit`方法。 但是，若要在调用 `SaveChanges` 失败时实现自定义错误消息，请将部分功能添加到此方法及其相应的视图中。

正如所看到的更新和创建操作，删除操作需要两个操作方法。 调用以响应 GET 请求的方法显示一个视图，使用户有机会批准或取消删除操作。 如果用户批准，则创建 POST 请求。 在这种情况， `HttpPost` `Delete`调用方法，然后该方法实际执行删除操作。

你将添加`try-catch`阻止`HttpPost``Delete`方法以处理更新数据库时可能出现的任何错误。 如果发生错误， `HttpPost` `Delete`方法调用`HttpGet``Delete`方法，并向其传递一个参数，指示发生错误。 `HttpGet Delete`方法然后重新显示确认页以及错误消息，为用户提供取消或稍后重试的机会。

1. 替换`HttpGet``Delete`用下面的代码，用于管理错误报告的操作方法： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    此代码接受[可选](https://msdn.microsoft.com/library/dd264739.aspx)布尔参数，用于指示是否它在无法保存更改之后调用。 此参数是`false`时`HttpGet``Delete`不上一次失败的情况下调用方法。 调用时`HttpPost``Delete`方法以响应数据库更新错误，该参数是`true`和一条错误消息传递给视图。
2. 替换`HttpPost``Delete`操作方法 (名为`DeleteConfirmed`) 使用以下代码，其执行实际删除操作并捕获任何数据库更新错误。

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     此代码检索所选的实体，然后调用[删除](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)方法将实体的状态设置为`Deleted`。 当`SaveChanges`调用时，SQL`DELETE`生成命令。 你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。 基架的代码名为`HttpPost``Delete`方法`DeleteConfirmed`以便`HttpPost`方法唯一的签名。 （CLR 要求重载的方法具有不同的方法参数。）签名是唯一的现在可以继续使用 MVC 约定，使用相同的名称`HttpPost`和`HttpGet`删除方法。

     如果在大容量应用程序中提高性能是优先考虑，可以避免不必要的 SQL 查询，若要检索的行替换为调用的代码行`Find`和`Remove`用下面的代码如黄色中所示的方法突出显示：

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     此代码实例化`Student`实体使用的主要密钥值然后将实体状态设置为`Deleted`。 这是 Entity Framework 删除实体需要执行的所有操作。

     如所述， `HttpGet` `Delete`方法不会删除数据。 执行删除操作以响应 GET 请求 （或者就此而言，执行的任何编辑操作，创建操作或更改数据的任何其他操作） 会产生安全风险。 有关详细信息，请参阅[ASP.NET MVC 提示 #46 — 不使用删除链接，因为他们创建的安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)Stephen Walther 的博客上。
3. 在中*Views\Student\Delete.cshtml*，添加一条错误消息之间`h2`标题和`h3`标题，如下面的示例中所示：

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     通过选择运行页**学生**选项卡并单击**删除**超链接：

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. 单击“删除”。 将显示不含已删除学生的索引页。 (您将看到的错误处理中的操作中的代码示例[处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列后面的教程。)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>确保数据库连接不会保持打开状态

若要确保能正确关闭数据库连接，并且它们具有了已释放的资源，您应该看到与其释放上下文实例。 基架的代码提供的就是为什么[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法的末尾`StudentController`类*StudentController.cs*，如以下示例所示：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

基`Controller`类已经实现`IDisposable`接口，所以此代码只需将添加到替代`Dispose(bool)`方法来显式释放上下文实例。

## <a name="summary"></a>总结

现在有了一整套的执行简单的 CRUD 操作执行的页`Student`实体。 MVC 帮助程序用于生成数据字段的 UI 元素。 MVC 帮助程序的详细信息，请参阅[呈现窗体使用 HTML 帮助程序](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx)（该页是为 MVC 3 但仍适用于 MVC 4）。

在下一教程将通过添加排序和分页来展开索引页的功能。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [下一页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
