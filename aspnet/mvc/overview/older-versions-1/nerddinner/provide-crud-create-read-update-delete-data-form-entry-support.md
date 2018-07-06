---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持 |Microsoft Docs
author: microsoft
description: 步骤 5 显示了如何通过启用支持编辑、 创建和使用它删除 Dinners 也使我们的 DinnersController 类进一步。
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: bfb8446ec8b39ad6fc88a0d5b747f0cec33bbd25
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817631"
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 5 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 5 显示了如何通过启用支持编辑、 创建和使用它删除 Dinners 也使我们的 DinnersController 类进一步。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 步骤 5： 创建、 更新、 删除窗体方案

我们引入了控制器和视图，并介绍如何使用它们来在站点上实现 Dinners 的列表/详细信息体验。 下一步将采取进一步的我们的 DinnersController 类，并启用对编辑、 创建和使用它还删除 Dinners 的支持。

### <a name="urls-handled-by-dinnerscontroller"></a>由 DinnersController 的 Url

我们之前添加操作方法向 DinnersController 实现对两个 Url 的支持： */Dinners*并 */Dinners/详细信息 / [id]*。

| **URL** | **VERB** | **目的** |
| --- | --- | --- |
| */Dinners/* | GET | 显示即将到来的 dinners 的 HTML 列表。 |
| */Dinners/Details/[id]* | GET | 显示有关特定 dinner 的详细信息。 |

我们现在将操作方法来实现三个其他 Url: <em>/Dinners/编辑 / [id]、 / Dinners/创建、</em>并<em>/Dinners/Delete / [id]</em>。 这些 Url 将启用对编辑现有 Dinners，创建新 Dinners 和删除 Dinners 的支持。

我们将支持与这些新的 Url 的 HTTP GET 和 HTTP POST 谓词交互。 HTTP GET 请求到以下 Url 将显示数据 （使用在"编辑"的情况下的 Dinner 数据填充窗体，在"创建"的情况下的空白窗体和在"删除"的情况下删除确认屏幕） 的初始 HTML 视图。 这些 url 的 HTTP POST 请求将保存/更新/删除 Dinner 数据中我们 DinnerRepository （和从数据库到）。

| **URL** | **VERB** | **目的** |
| --- | --- | --- |
| */Dinners/Edit/[id]* | GET | 显示可编辑 HTML 窗体使用 Dinner 数据填充。 |
| 发布 | 保存到数据库的晚餐窗体更改。 |
| */Dinners/Create* | GET | 显示一个空的 HTML 窗体，用户可定义新 Dinners。 |
| 发布 | 创建新的 Dinner 并将其保存在数据库中。 |
| */Dinners/Delete/[id]* | GET | 显示删除确认屏幕。 |
| 发布 | 从数据库中删除指定的 dinner。 |

### <a name="edit-support"></a>编辑支持

让我们首先将实现"编辑"方案。

#### <a name="the-http-get-edit-action-method"></a>HTTP GET 编辑操作方法

我们将首先实现我们的编辑操作方法的 HTTP"GET"行为。 此方法将调用何时 */Dinners/编辑 / [id]* 请求 URL。 我们的实现将如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上面的代码使用 DinnerRepository 检索 Dinner 对象。 然后，它将呈现视图模板使用 Dinner 对象。 因为我们尚未显式传递到的模板名称*View()* 帮助器方法，它将使用的约定，其默认路径来解析视图模板： /Views/Dinners/Edit.aspx。

让我们现在创建此视图模板。 我们将编辑方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给视图模板作为它的模型，并选择"编辑"的模板自动基架：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

当我们单击"添加"按钮时，Visual Studio 将"\Views\Dinners"目录中为我们添加新的"Edit.aspx"视图模板文件。 它还会打开新的"Edit.aspx"视图模板代码的编辑器 – 填充初始"的编辑"基架实现如下下面内：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

让我们进行一些更改到默认"的编辑"基架生成，并更新具有以下内容 （从而删除几个我们不想要公开的属性） 的编辑视图模板：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

当我们运行的应用程序和请求 *"/ Dinners/编辑/1"* 我们将看到以下页面的 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

视图生成的 HTML 标记类似于下面。 这一点与标准 HTML –&lt;窗体&gt;执行 HTTP POST 到的元素 */Dinners/Edit/1* URL 时"保存" &lt;type ="提交"/&gt;按钮。 在 HTML &lt;type ="text"/&gt;元素已为每个可编辑的属性的输出：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() 和 Html.TextBox() 的 Html 帮助器方法

我们"Edit.aspx"视图模板正在使用的多个"的 Html 帮助器"方法： Html.ValidationSummary()、 Html.BeginForm()、 Html.TextBox() 和 Html.ValidationMessage()。 除了为我们生成的 HTML 标记，这些帮助器方法提供了内置的错误处理和验证支持。

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() 帮助器方法

Html.BeginForm() 帮助程序方法是 HTML 输出内容是什么&lt;窗体&gt;我们标记中的元素。 我们 Edit.aspx 视图模板中您会注意到，我们要将应用的 C#"using"语句时使用此方法。 左大括号指示的开头&lt;窗体&gt;内容和右大括号是所指示的结束&lt;/&gt;元素：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

或者，如果你发现"using"语句方法不自然的此类方案，您可以使用 Html.BeginForm() 和 Html.EndForm() 的组合 （这会执行相同的操作）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

不带任何参数调用 Html.BeginForm() 会让其输出到当前请求的 URL 执行 HTTP POST 的窗体元素。 编辑视图生成的它是为什么*&lt;表单操作 ="/ Dinners/编辑/1"方法 ="post"&gt;* 元素。 我们无法具有或者传递显式参数给 Html.BeginForm() 如果我们想要发布到不同的 URL。

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() 帮助器方法

Edit.aspx 视图使用 Html.TextBox() 帮助器方法来输出&lt;type ="text"/&gt;元素：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上面的 Html.TextBox() 方法采用单个参数 – 用于指定的 id/name 特性&lt;type ="text"/&gt;输出，以及要填充的文本框值的模型属性的元素。 例如，我们传递给编辑视图的 Dinner 对象具有".NET Future"的"Title"属性值，因此我们 Html.TextBox("Title") 方法调用输出： *&lt;输入的 id ="Title"名称 ="Title"type ="text"value =".NET Futures"/&gt;*.

或者，我们可以使用第一个 Html.TextBox() 参数来指定 id/名称的元素，并显式传递值中要用作第二个参数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

通常，我们需要执行的输出值的自定义格式设置。 内置于.NET string.format （) 的静态方法可用于这些方案。 我们 Edit.aspx 视图模板使用此 EventDate 值 （这是类型为 DateTime 的） 的格式设置，以便它不会显示时间 （秒）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html.TextBox() 的第三个参数 （可选） 用于输出其他 HTML 特性。 的以下代码段演示如何呈现其他大小 ="30"属性和 class ="mycssclass"属性上&lt;输入类型 ="text"/&gt;元素。 请注意，我们如何转义的类属性使用名称"@" character because "类"是保留的关键字在 C# 中：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>实现 HTTP POST 编辑操作方法

现在，我们实现我们编辑操作方法的 HTTP GET 版本。 当用户请求 */Dinners/Edit/1*他们收到如下所示的 HTML 页面的 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

按"保存"按钮会导致窗体发布到 */Dinners/Edit/1* URL，并将其提交 HTML&lt;输入&gt;窗体上使用 HTTP POST 谓词值。 现在让我们来实现我们编辑操作方法-保存 Dinner 将处理的 HTTP POST 行为。

我们将首先将重载的"编辑"操作方法添加到对其具有"AcceptVerbs"属性，指示它将处理 HTTP POST 方案我们 DinnersController:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

当 [AcceptVerbs] 特性应用于重载的操作方法时，ASP.NET MVC 将自动处理将请求调度到相应的操作方法，具体取决于传入的 HTTP 谓词。 HTTP POST 请求到<em>/Dinners/编辑 / [id]</em> Url 将转到上面的编辑方法，同时对所有其他 HTTP 谓词请求<em>/Dinners/编辑 / [id]</em>Url 将转到第一个编辑方法我们实现 （它未不具有 [AcceptVerbs] 特性）。

| **端主题： 为什么通过 HTTP 谓词区分？** |
| --- |
| 您可能会问 – 为什么是我们使用一个 URL 并且个性化的 HTTP 谓词通过其行为？ 为什么不只是具有两个不同的 Url 可以加载和保存的编辑更改？ 例如： /Dinners/编辑 / [id] 若要显示初始表单和 /Dinners/保存 / [id] 来处理窗体发布，将其保存？ 与发布两个不同的 Url 的缺点是，在其中我们发布到 /Dinners/Save/2，，然后需要重新 HTML 窗体显示由于输入错误的情况下，最终用户将最终 （因为这是在其浏览器地址栏中拥有 Dinners/保存/2 URLURL 发布到窗体)。 如果最终用户创建一个书签，本页 redisplayed 到用户浏览器的收藏夹列表，或复制/粘贴该 URL 和电子邮件发送给朋友，它们将得到保存 （因为该 URL 依赖于 post 值） 不会在将来工作的 URL。 通过公开一个 URL (例如： /Dinners/Edit/[id]) 并且个性化的处理它的 HTTP 谓词，它是安全的最终用户可以编辑页面加入书签和/或将 URL 发送给其他人。 |

#### <a name="retrieving-form-post-values"></a>检索窗体发布值

有多种方式我们就可以访问发布窗体中"的编辑"我们 HTTP POST 方法的参数。 一个简单的方法是只需使用控制器基类上的请求属性来访问窗体集合和直接检索已发布的值：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

不过，尤其是后我们将添加错误处理逻辑，上述方法是有些繁琐。

一个更好的方法了这种情况，可以利用内置*UpdateModel()* 控制器基类上的帮助器方法。 它支持更新的属性，我们将它使用传入的窗体参数传递的对象。 它使用反射来确定对对象的属性名称会自动将转换并将值分配给这些客户端提交的输入值。

我们可以使用 UpdateModel() 方法来简化使用此代码我们 HTTP POST 编辑操作：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

我们现在可以访问 */Dinners/Edit/1* URL，并更改我们 Dinner 标题：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

当我们单击"保存"按钮时，我们将执行窗体发布到我们的编辑操作，并更新后的值将保留在数据库中。 我们将随后重定向到详细信息 URL 为 Dinner （这将显示新保存的值）：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>处理编辑错误

我们当前的 HTTP POST 实现 works 微调 – 除非有错误。

当用户编辑窗体的一个错误，我们需要确保窗体将重新显示信息性错误消息，指导他们要修复此错误。 这包括最终用户在其中发布输入不正确的情况下 (例如： 的格式不正确的日期字符串)，如事例以及输入的格式是否有效，但没有业务规则冲突。 出现错误时在窗体应保留输入的数据最初输入，以便他们不需要手动重新填充其更改的用户。 窗体已成功完成之前，应根据需要多次重复此过程。

ASP.NET MVC 包括一些不错的内置功能，可使错误处理和窗体起简单。 若要查看操作中的这些功能，让我们使用以下代码更新我们的编辑操作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上面的代码类似于我们以前的实现 – 只是我们现在包装在 try/catch 错误处理块围绕我们的工作。 调用 UpdateModel()，或在我们尝试并保存 DinnerRepository （这将引发异常，如果我们尝试保存的 Dinner 对象是无效的由于我们的模型中的规则冲突），如果发生异常时将我们 catch 错误处理块执行。 在其中我们循环访问 Dinner 对象中存在任何规则冲突，并将其添加到 ModelState 对象 （我们将稍后讨论）。 然后，我们重新显示该视图。

若要查看此工作让我们重新运行该应用程序，编辑 Dinner，并将其更改为具有空标题，EventDate"BOGUS"，并使用美国国家/地区值为英国电话号码。 当我们按"保存"按钮时我们编辑 HTTP POST 方法将不能保存 Dinner （因为有错误） 以及将重新显示该窗体：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

我们的应用程序具有适当的错误体验。 具有无效的输入的文本元素突出显示为红色，并向最终用户有关其显示验证错误消息。 在窗体还保留用户最初输入 – 的输入的数据，以便他们无需重新填充任何内容。

如何，您可能会问，这发生一样？ 如何没有 Title、 EventDate 和 contactphone 文本框以红色突出显示本身并知道要输出的最初输入的用户值？ 和如何未显示错误消息获取顶部列表中？ 值得高兴的是，这并不发生变魔术一样-而是因为我们使用一些内置的 ASP.NET MVC 功能，使输入的验证和错误处理方案轻松。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>了解 ModelState 和验证的 HTML 帮助器方法

控制器类具有一个"ModelState"属性集合，它提供了一种方法，以指示错误存在与传递给视图的模型对象。 ModelState 集合中的错误条目与问题标识模型属性的名称 (例如:"Title"、"EventDate"或"ContactPhone")，并允许指定的用户友好错误消息 (例如:"标题是必需的")。

*UpdateModel()* 帮助器方法尝试将窗体值分配给模型对象的属性时遇到错误时自动填充 ModelState 集合。 例如，我们的 Dinner 对象 EventDate 属性是 DateTime 类型。 当 UpdateModel() 方法不能为其分配的字符串值"BOGUS"，在上述方案中时，UpdateModel() 方法添加到表示分配错误的错误的 ModelState 集合的一个条目发生与该属性。

开发人员还可以编写代码以显式添加到 ModelState 集合错误条目，像我们在下面我们"捕获"错误处理块内，这使用基于中活动的规则冲突项填充 ModelState 集合Dinner 对象：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>与 ModelState 的 html 帮助器集成

呈现输出时，HTML 帮助器方法-如 Html.TextBox()-检查 ModelState 集合。 如果存在错误的项，它们呈现用户输入值和 CSS 错误类。

例如，"编辑"视图中我们使用 Html.TextBox() 帮助器方法呈现的我们的 Dinner 对象 EventDate:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

错误方案中呈现视图时，Html.TextBox() 方法将检查以查看是否存在与我们的 Dinner 对象"EventDate"属性相关联的任何错误的 ModelState 集合。 当不确定时出错它将呈现提交的用户输入 ("BOGUS") 作为值，并添加 css 错误类中的，以便&lt;type ="textbox"/&gt;它生成的标记：

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

您可以自定义要查找但是您希望 css 错误类的外观。 中定义的默认 CSS 错误类 –"输入的验证错误"– *\content\site.css*样式表和看起来如下所示：

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

此 CSS 规则是什么导致我们无效的输入的元素，如下面突出显示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() 帮助器方法

Html.ValidationMessage() 帮助器方法可用于输出与特定的模型属性关联的 ModelState 错误消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上述代码输出：  *&lt;/><span class ="字段的验证错误"&gt;是无效的值 BOGUS &lt; /s p a n&gt;*

Html.ValidationMessage() 帮助器方法还支持允许开发人员重写为显示的错误文本消息的第二个参数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上述代码输出：  <em>&lt;/><span class ="字段的验证错误"&gt;\*&lt;/s p a n&gt;</em>而不是时出现错误时，将提供的默认错误文本EventDate 属性。

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() 帮助器方法

Html.ValidationSummary() 帮助器方法可用于呈现摘要错误消息，伴随&lt;ul&gt;&lt;li /&gt;&lt;/u l&gt;消息中的所有详细的错误列表ModelState 集合：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.ValidationSummary() 帮助程序方法采用一个可选的字符串参数 – 用于定义要显示详细的错误列表上方的摘要错误消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

您可以选择使用 CSS 来重写错误列表如下所示。

#### <a name="using-a-addruleviolations-helper-method"></a>使用 AddRuleViolations 帮助器方法

我们的初始 HTTP POST 编辑实现使用它的 catch 块中的 foreach 语句循环访问 Dinner 对象的规则冲突，并将其添加到控制器的 ModelState 集合：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

我们可以使此代码通过添加"ControllerHelpers"小更加清晰明确到 NerdDinner 项目中，类，实现"AddRuleViolations"扩展方法在其中将一个帮助器方法添加到 ASP.NET MVC ModelStateDictionary 类。 此扩展方法可以封装填充 ModelStateDictionary RuleViolation 错误的列表所需的逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

然后，我们可以更新我们编辑 HTTP POST 操作方法使用此扩展方法来填充我们 Dinner 规则冲突的 ModelState 集合。

#### <a name="complete-edit-action-method-implementations"></a>完成编辑操作的方法实现

下面的代码实现了所有我们的编辑方案所需的控制器逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

我们的编辑实现好处是，我们的控制器类和视图模板都不必须完全了解特定验证或通过我们的 Dinner 模型强制实施的业务规则。 我们可以将其他规则在将来添加到我们的模型并不需要对我们的控制器或视图以使其支持进行任何代码更改。 这为我们提供了灵活地可以方便地改进我们的应用程序要求在将来使用最少代码更改。

### <a name="create-support"></a>创建的支持

我们已实现我们的 DinnersController 类的"编辑"行为。 让我们继续操作，以便可对其 – 这将使用户能够添加新 Dinners"创建"支持。

#### <a name="the-http-get-create-action-method"></a>HTTP GET 创建操作方法

我们将首先实现 HTTP"GET"行为的我们创建操作方法。 在有人访问时，将调用此方法 */Dinners/创建*URL。 我们的实现如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上面的代码创建一个新的 Dinner 对象，并分配其 EventDate 属性设置为在将来的一周。 然后，它将呈现一个视图，它基于新的 Dinner 对象。 因为我们尚未显式传递将名称传递给*View()* 帮助器方法，它将使用的约定，其默认路径来解析视图模板： /Views/Dinners/Create.aspx。

让我们现在创建此视图模板。 我们可以创建操作方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作。 在"添加视图"对话框中，我们将指示我们要将 Dinner 对象传递给视图模板，然后选择自动基架"创建"模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

当我们单击"添加"按钮时，Visual Studio 会将新的基架基于"Create.aspx"视图保存到"\Views\Dinners"目录，并在 IDE 中打开它：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

让我们对我们而言，到默认"创建"基架生成的文件已进行一些更改，并向上修改要看到如下所示：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

现在，当我们运行我们的应用程序和访问权限和 *"/ Dinners/创建"* 它会从我们创建的操作实现呈现 UI 中的，如下面的浏览器中的 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>创建实现 HTTP POST 操作方法

我们已实现我们创建操作方法的 HTTP GET 版本。 当用户单击"保存"按钮时它会执行窗体发布到 */Dinners/创建*URL，并将其提交 HTML&lt;输入&gt;窗体上使用 HTTP POST 谓词值。

让我们现在实现 HTTP POST 行为的我们创建操作方法。 我们将首先将重载的"创建"操作方法添加到对其具有"AcceptVerbs"属性，指示它将处理 HTTP POST 方案我们 DinnersController:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

有多种方式可以访问已发布的表单参数中我们的 HTTP POST 启用"创建"方法。

一种方法是创建一个新的 Dinner 对象，然后使用*UpdateModel()* 帮助器方法 （如我们所做的编辑操作） 要使用已发布的表单值填充它。 我们然后可以将其添加到我们 DinnerRepository、 将其保存到数据库，并将用户重定向到我们的详细信息操作以显示新创建的 Dinner 使用下面的代码：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

或者，我们可以使用一种方法还有我们采用 Dinner 对象作为方法参数的 create （） 操作方法。 ASP.NET MVC 将自动为我们实例化一个新的 Dinner 对象、 填充其属性使用窗体的输入，并将其传递给我们的操作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

我们上面的操作方法验证，Dinner 对象成功填充窗体发布值与通过检查 ModelState.IsValid 属性。 这将返回 false，如果有输入转换问题 (例如： EventDate 属性"BOGUS"的字符串)，并且如果有任何问题我们操作方法重新显示该窗体。

如果输入的值都有效，操作方法就尝试添加并将新的 Dinner 保存到 DinnerRepository。 它包装这项工作在 try/catch 块内的，并重新显示该窗体，如果有任何业务规则冲突 （这会导致 dinnerRepository.Save() 方法来引发异常）。

若要查看此错误处理操作中的行为，我们可以请求 */Dinners/创建*URL 和有关新 Dinner 的详细信息，请填写。 输入不正确或值将导致创建窗体以重新显示如以下突出显示的错误：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

请注意，我们创建窗体如何遵循确切相同验证和业务规则作为我们的编辑窗体。 这是因为我们验证和业务规则在模型中，定义和未嵌入在 UI 或应用程序的控制器中。 这意味着我们可以稍后更改/改进我们验证或在单个的业务规则放置，并将它们应用于整个应用程序。 我们不会更改任何代码中的我们编辑或创建操作方法来自动接受任何新的规则或对现有的修改。

我们修复输入的值并单击"保存"按钮时同样，我们加入 DinnerRepository 将成功，并且新 Dinner 将添加到数据库。 我们随后重定向到 */Dinners/详细信息 / [id]* URL – 其中我们将提供有关新创建的 Dinner 的详细信息：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>删除支持

让我们现在添加到我们 DinnersController 的"删除"支持。

#### <a name="the-http-get-delete-action-method"></a>HTTP GET Delete 操作方法

我们将首先实现我们的 delete 操作方法的 HTTP GET 行为。 在有人访问时，将会调用此方法 */Dinners/Delete / [id]* URL。 下面是实现：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

尝试检索 Dinner 要删除的操作方法。 如果 Dinner 存在，则呈现视图基于 Dinner 对象。 如果对象不存在 （或已被删除） 它返回一个视图，它将呈现"NotFound"查看我们以前为我们的"详细信息"操作方法创建的模板。

我们可以创建"删除"查看模板的 Delete 操作方法内右键单击并选择"添加视图"上下文菜单命令。 在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给视图模板作为它的模型，并选择创建一个空的模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

当我们单击"添加"按钮时，Visual Studio 将我们"\Views\Dinners"目录中为我们添加新的"Delete.aspx"视图模板文件。 我们将向模板来实现删除确认屏幕中添加一些 HTML 和代码如下所示：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上面的代码显示的标题，Dinner 要删除，然后输出&lt;窗体&gt;执行 POST 到 /Dinners/Delete / [id] URL，如果最终用户单击"删除"按钮中的元素。

当我们运行我们的应用程序和访问 *"/ Dinners/Delete / [id]"* URL 有效 Dinner 对象它呈现用户界面与下面类似：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **端主题： 我们为何做一个帖子？** |
| --- |
| 您可能会问 – 我们为何做通过创建的工作量&lt;窗体&gt;我们删除确认屏幕中？ 为什么不直接使用标准的超链接链接到操作方法执行实际删除操作？ 原因是因为我们想要小心操作以防范 web 爬网程序，搜索引擎发现了 Url 和无意中导致当他们单击链接时要删除的数据。 基于 HTTP GET 的 Url 被视为"安全"才能访问/爬网，并且它们应该遵循 HTTP POST 的。 很好的规则是，请确保您始终将放在破坏性或数据修改操作背后的 HTTP POST 请求。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>实现 HTTP POST Delete 操作方法

现在，我们实现我们 Delete 操作方法的 HTTP GET 版本显示删除确认屏幕。 当最终用户单击"删除"按钮时它将执行到窗体发布 */Dinners/Dinner / [id]* URL。

让我们现在实现的 HTTP"POST"行为的 delete 操作方法使用下面的代码：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

我们删除操作方法的 HTTP POST 版本尝试检索要删除的 dinner 对象。 如果它找不到它 （因为它已被删除） 将呈现"NotFound"模板。 如果找到 Dinner，它可以从 DinnerRepository 删除它。 然后，它将呈现"已删除"模板。

若要实现我们将在操作方法中右键单击并选择"添加视图"上下文菜单的"已删除"模板。 我们将命名为"已删除"视图，并将它是一个空的模板 （并且不采用强类型化模型对象）。 然后，我们将向其中添加一些 HTML 内容：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

现在，当我们运行我们的应用程序和访问权限和 *"/ Dinners/Delete / [id]"* URL 有效 dinner 对象，它会呈现我们 Dinner 删除确认屏幕类似如下：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

当我们单击"删除"按钮时它将执行到 HTTP POST */Dinners/Delete / [id]* URL，这将删除 Dinner 从我们的数据库，并显示"已删除"视图模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>模型绑定安全性

我们已经讨论了两种不同方式使用内置的 ASP.NET MVC 模型绑定功能。 首先使用 UpdateModel() 方法来更新现有的模型对象，属性和第二个使用对作为操作方法参数传递中的模型对象的 ASP.NET MVC 支持。 这两种方法是非常强大和极其有用。

这种能力还提供了责任。 很重要的始终是有关安全性的警惕用户如果接受任何用户输入，并且这也是 true 时将对象绑定到窗体输入。 应为请注意，始终 HTML 编码以避免 HTML 和 JavaScript 注入攻击，并请注意 SQL 注入式攻击的任何用户输入值 (注意： 我们在我们的应用程序，它会自动将编码参数，防止这些使用 LINQ to SQL类型的攻击）。 永远不应依赖于客户端验证独立的并始终使用服务器端验证，可防止黑客试图向你发送虚假的值来。

要确保你考虑使用 ASP.NET MVC 的绑定功能时的一个额外的安全项是要绑定的对象的作用域。 具体而言，你想要确保你了解你允许将绑定，并确保只允许那些实际上应为要更新的最终用户可更新的属性的属性的安全隐患。

默认情况下，UpdateModel() 方法将尝试更新对模型对象与传入的窗体参数值匹配的所有属性。 同样，为操作方法参数还默认传递的对象可以具有所有通过窗体参数设置其属性。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>锁定在每个使用情况的基础上的绑定

你可以通过提供一个显式"include 列表"的可更新的属性来锁定在每个使用情况的基础上的绑定策略。 这可以通过将额外的字符串数组参数传递给 UpdateModel() 类似方法的下方：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

此外为操作方法参数传递的对象支持 [Bind] 属性，它使一个"include 列表"的允许使用属性来指定类似如下：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>锁定类型基础上的绑定

你可以锁定在每种类型的基础上的绑定规则。 这允许您一次，指定绑定规则，然后让其在所有控制器和操作方法适合所有情况 （包括 UpdateModel 和操作方法参数方案）。

通过添加到类型上的 [Bind] 属性或通过注册 （适用于其中的类型不属于你的方案） 的应用程序的 Global.asax 文件中，可以自定义每种类型的绑定规则。 然后，可以使用的绑定属性的 Include 和 Exclude 属性来控制哪些属性是可绑定为特定类或接口。

我们将 Dinner 类在 NerdDinner 应用程序中，使用这种方法，并将 [Bind] 属性添加到它的可绑定属性的列表限制到以下：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

请注意，我们不允许 Rsvp 集合操作通过绑定，也不我们允许 DinnerID 或 HostedBy 属性通过绑定设置。 出于安全原因我们将改为仅控制这些特定属性使用在我们的操作方法中的显式代码。

### <a name="crud-wrap-up"></a>CRUD 总结

ASP.NET MVC 包括大量内置功能，帮助实现窗体发布方案。 我们使用了各种各样的这些功能在我们 DinnerRepository 之上提供 CRUD UI 支持。

我们使用的专注于模型的方法来实现我们的应用程序。 这意味着，我们所有的验证和业务规则中我们的模型层 – 而不是在我们的控制器或视图定义逻辑。 我们的控制器类和我们的视图模板都不知道我们 Dinner model 类通过强制实施的特定业务规则有关的任何信息。

这将使我们的应用程序体系结构保持干净，并使其更易于测试。 我们可以将更多的业务规则在将来添加到我们的模型层和*无需进行任何代码更改*到我们的控制器或视图以使其支持。 这将向我们提供了大量的改进和更改在将来，我们的应用程序的灵活性。

我们 DinnersController 现在使 Dinner 列表/详细信息，以及创建、 编辑和删除支持。 类的完整代码可在下文：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>下一步

现在，我们有我们 DinnersController 类中实现的基本 CRUD （创建、 读取、 更新和删除） 支持。

让我们现在看一下如何使用 ViewData 和 ViewModel 类要在窗体上启用更丰富的 UI。

> [!div class="step-by-step"]
> [上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)
