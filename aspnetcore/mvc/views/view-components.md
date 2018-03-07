---
title: "视图组件"
author: rick-anderson
description: "视图组件可用于具有可重用呈现逻辑的任何位置。"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/view-components
ms.openlocfilehash: 65074ca02a1365db278d348d4e024121a6eb4634
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="view-components"></a>视图组件

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="introducing-view-components"></a>视图组件简介

作为 ASP.NET Core MVC 的新功能，视图组件与分部视图类似，但它们的功能更加强大。视图组件不使用模型绑定，并且仅依赖调用时提供的数据。视图组件：

* 呈现一个块，而不是整个响应
* 包括的相同问题分离和控制器和视图之间找到的可测试性优势
* 可以具有参数和业务逻辑
* 从布局页通常会对其进行调用

视图组件可用于具有可重用呈现逻辑（对分部视图来说过于复杂）的任何位置，例如：

* 动态导航菜单
* 标记云（查询数据库的位置）
* 登录面板
* 购物车
* 最近发布的文章
* 典型的博客上的侧栏内容
* 一个登录面板，呈现在每页上并显示注销或登录链接，具体取决于用户的登录状态

视图组件由两部分组成：类（通常派生自 [ViewComponent](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.viewcomponent)）及其返回的结果（通常为视图）。与控制器一样，视图组件也可以是 POCO，但大多数开发人员都希望利用派生自 `ViewComponent` 的可用方法和属性。

## <a name="creating-a-view-component"></a>创建视图组件

本部分包含创建视图组件的高级别要求。本文后续部分将详细检查每个步骤并创建视图组件。

### <a name="the-view-component-class"></a>视图组件类

可通过以下任一方法创建视图组件类：

* 派生自*ViewComponent*
* 修饰具有的类`[ViewComponent]`属性，或从具有的类派生`[ViewComponent]`属性
* 创建名称以 ViewComponent 后缀结尾的类

与控制器一样，视图组件必须是公共、非嵌套和非抽象的类。视图组件名称是删除了“ViewComponent”后缀的类名。也可以使用 `ViewComponentAttribute.Name` 属性显式指定它。

视图组件类：

* 完全支持构造函数[依赖关系注入](../../fundamentals/dependency-injection.md)

* 在控制器生命周期，这意味着你无法使用不带一部分[筛选器](../controllers/filters.md)视图组件中

### <a name="view-component-methods"></a>视图组件方法

视图组件以返回 `IViewComponentResult` 的 `InvokeAsync` 方法定义其逻辑。参数直接来自视图组件的调用，而不是来自模型绑定。视图组件从不直接处理请求。通常，视图组件通过调用 `View` 方法来初始化模型并将其传递到视图。总之，视图组件方法：

* 定义返回 `IViewComponentResult` 的 `InvokeAsync` 方法
* 通常初始化模型并将其传递到视图，通过调用`ViewComponent``View`方法
* 参数来自调用的方法中，不是 HTTP，没有任何模型绑定
* 不可直接作为 HTTP 终结点访问，它们从代码调用（通常在视图中）。视图组件从不处理请求
* 在签名而不是当前 HTTP 请求中的任何详细上重载

### <a name="view-search-path"></a>视图搜索路径

运行时中搜索以下路径中的视图：

   * Views/\<controller_name>/Components/\<view_component_name>/\<view_name>
   * Views/Shared/Components/\<view_component_name>/\<view_name>

视图组件的默认视图名称为“默认”**，这意味着视图文件通常命名为“Default.cshtml”**。可以在创建视图组件结果或调用 `View` 方法时指定不同的视图名称。

建议将视图文件命名为“Default.cshtml”**并使用 *Views/Shared/Components/\<view_component_name > /\<view_name >* 路径。此示例中使用的 `PriorityList` 视图组件对视图组件视图使用 *Views/Shared/Components/PriorityList/Default.cshtml*。

## <a name="invoking-a-view-component"></a>调用视图组件

若要使用视图组件，请调用以下命令，在视图内：

```cshtml
@Component.InvokeAsync("Name of view component", <anonymous type containing parameters>)
```

参数将传递给`InvokeAsync`方法。 `PriorityList`视图在文章中开发的组件调用从*Views/Todo/Index.cshtml*视图文件。 在下面的示例，`InvokeAsync`方法调用包含两个参数：

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

## <a name="invoking-a-view-component-as-a-tag-helper"></a>调用视图组件作为标记帮助器

有关 ASP.NET 核心 1.1 和更高版本，你可以调用将视图组件作为[标记帮助器](xref:mvc/views/tag-helpers/intro):

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

有关标记帮助程序 Pascal 大小写形式类和方法的参数转换为其[降低 kebab 用例](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101)。 用于调用视图组件标记帮助程序使用`<vc></vc>`元素。 视图组件按如下方式指定：

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

注意： 若要将视图组件用作标记帮助程序，你必须注册包含视图组件使用的程序集`@addTagHelper`指令。 例如，如果你视图组件是一个程序集称为"MyWebApp"中，添加以下指令到`_ViewImports.cshtml`文件：

```cshtml
@addTagHelper *, MyWebApp
```

可以将视图组件注册为引用视图组件任何文件标记帮助器。 请参阅[管理标记帮助器作用域](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope)有关如何注册标记帮助器的详细信息。

`InvokeAsync`本教程中使用的方法：

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

在标记帮助器标记：

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

在以上示例中，`PriorityList` 视图组件变为 `priority-list`。视图组件的参数作为小写短横线格式的属性进行传递。

### <a name="invoking-a-view-component-directly-from-a-controller"></a>直接从控制器调用视图组件

视图组件通常从视图调用，但你可以直接从控制器方法调用它们。尽管视图组件不定义控制器等终结点，但你可以轻松实现返回 `ViewComponentResult` 内容的控制器操作。

在此示例中，直接从控制器中调用视图组件：

[!code-csharp[Main](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a>演练： 创建简单视图组件

[下载](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)、 生成和测试起始代码。 它是使用一个简单项目`Todo`显示的列表的控制器*Todo*项。

![ToDos 的列表](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a>添加 ViewComponent 类

创建*ViewComponents*文件夹并添加以下`PriorityListViewComponent`类：

[!code-csharp[Main](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

代码的说明：

* 视图组件类可包含在**任何**项目中的文件夹。
* 因为的类名称 PriorityList**ViewComponent**以后缀结尾**ViewComponent**，从视图中引用类组件时，运行时将使用字符串"PriorityList"。 我将介绍的更详细地更高版本。
* `[ViewComponent]`属性可以更改用来引用视图组件的名称。 例如，我们无法已命名类`XYZ`和应用`ViewComponent`属性：

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* `[ViewComponent]`上面属性告知视图组件选择器，以使用名称`PriorityList`查找关联与该组件，并从视图中引用类组件时使用字符串"PriorityList"的视图时。 我将介绍的更详细地更高版本。
* 该组件使用[依赖关系注入](../../fundamentals/dependency-injection.md)要提供的数据上下文。
* `InvokeAsync`公开可以从视图中，和它调用的方法可以采用任意数量的自变量。
* `InvokeAsync`方法返回的一套`ToDo`符合项`isDone`和`maxPriority`参数。

### <a name="create-the-view-component-razor-view"></a>创建视图组件 Razor 视图

* 创建 *Views/Shared/Components* 文件夹。此文件夹**必须**命名为“Components”**。

* 创建*Views/Shared/Components/PriorityList*文件夹。 此文件夹名称必须与视图组件类的名称或减后缀类的名称匹配 (如果我们遵循约定，并且使用*ViewComponent*中的类名称后缀)。 如果你使用`ViewComponent`属性，类名称需要匹配所指定的属性。

* 创建*Views/Shared/Components/PriorityList/Default.cshtml* Razor 视图：[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]
    
   Razor 查看所花费的列表`TodoItem`并显示它们。 如果视图组件`InvokeAsync`方法不满足 （如我们的示例），视图的名称*默认*由用于约定的视图名称。 更高版本在教程中，我将向你演示如何将传递视图的名称。 若要覆盖特定控制器的默认样式，请将视图添加到特定于控制器的视图文件夹 (例如*Views/Todo/Components/PriorityList/Default.cshtml)*。
    
    如果控制器特定视图组件，则你可以将其添加到特定于控制器的文件夹 (*Views/Todo/Components/PriorityList/Default.cshtml*)。

* 添加`div`包含到底部的优先级列表组件调用*Views/Todo/index.cshtml*文件：

    [!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFirst.cshtml?range=34-38)]

标记 `@await Component.InvokeAsync` 显示调用视图组件的语法。第一个参数是要调用的组件的名称。后续参数将传递给该组件。`InvokeAsync` 可以采用任意数量的参数。

测试应用程序。 下图显示 ToDo 列表和优先级的项：

![todo 列表和优先级项](view-components/_static/pi.png)

你还可以直接从控制器调用视图组件：

[!code-csharp[Main](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![优先级的项从 IndexVC 操作](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a>指定的视图名称

在某些情况下，复杂的视图组件可能需要指定非默认视图。以下代码显示如何从 `InvokeAsync` 方法指定“PVC”视图。更新 `PriorityListViewComponent` 类中的 `InvokeAsync` 方法。

[!code-csharp[Main](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

复制*Views/Shared/Components/PriorityList/Default.cshtml*文件到名为视图*Views/Shared/Components/PriorityList/PVC.cshtml*。 添加标题以指示正在使用 PVC 视图。

[!code-cshtml[Main](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

更新*Views/TodoList/Index.cshtml*:

<!-- Views/TodoList/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

运行应用程序并验证 PVC 视图。

![优先级视图组件](view-components/_static/pvc.png)

如果不呈现 PVC 视图，请验证正在调用的优先级为 4 或更高版本的视图组件。

### <a name="examine-the-view-path"></a>检查视图路径

* 将优先级参数更改为三个或更少因此 priority 视图不返回。
* 暂时重命名*Views/Todo/Components/PriorityList/Default.cshtml*到*1Default.cshtml*。
* 测试应用程序，您将收到以下错误：

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' wasn't found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* 复制*Views/Todo/Components/PriorityList/1Default.cshtml*到*Views/Shared/Components/PriorityList/Default.cshtml*。
* 添加到一些标记*共享*Todo 视图组件视图，以指示该视图是从*共享*文件夹。
* 测试**共享**组件视图。

![与共享组件视图 ToDo 输出](view-components/_static/shared.png)

### <a name="avoiding-magic-strings"></a>避免神奇的字符串

若要确保编译时的安全性，可以用类名替换硬编码的视图组件名称。创建没有“ViewComponent”后缀的视图组件：

[!code-csharp[Main](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

将 `using` 语句添加到 Razor 视图文件，并使用 `nameof` 运算符：

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexNameof.cshtml?range=1-6,33-)]

## <a name="additional-resources"></a>其他资源

* [视图中的依赖关系注入](dependency-injection.md)
