---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 检查 ASP.NET MVC 如何支持 DropDownList 帮助程序 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: ece3645f2b37550058a5c93bdd9badbc088ae11c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382960"
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="287a9-102">检查 ASP.NET MVC 如何支持 DropDownList 帮助程序</span><span class="sxs-lookup"><span data-stu-id="287a9-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>
====================
<span data-ttu-id="287a9-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="287a9-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="287a9-104">在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。</span><span class="sxs-lookup"><span data-stu-id="287a9-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="287a9-105">将控制器命名**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="287a9-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="287a9-106">设置的选项**添加控制器**对话框如下图所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="287a9-107">编辑*StoreManager\Index.cshtml*查看和删除`AlbumArtUrl`。</span><span class="sxs-lookup"><span data-stu-id="287a9-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="287a9-108">删除`AlbumArtUrl`使演示文稿更具可读性。</span><span class="sxs-lookup"><span data-stu-id="287a9-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="287a9-109">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="287a9-110">打开*Controllers\StoreManagerController.cs*文件并查找`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="287a9-111">添加`OrderBy`子句，以便将价格按排序唱片集。</span><span class="sxs-lookup"><span data-stu-id="287a9-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="287a9-112">完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="287a9-113">价格按排序将更加轻松地测试对数据库进行更改。</span><span class="sxs-lookup"><span data-stu-id="287a9-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="287a9-114">时测试编辑和创建方法，可以使用较低的价格，因此已保存的数据将显示第一个。</span><span class="sxs-lookup"><span data-stu-id="287a9-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="287a9-115">打开*StoreManager\Edit.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="287a9-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="287a9-116">恰好在图例标记之后添加以下行。</span><span class="sxs-lookup"><span data-stu-id="287a9-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="287a9-117">下面的代码显示了此更改的上下文：</span><span class="sxs-lookup"><span data-stu-id="287a9-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="287a9-118">`AlbumId`需对唱片集记录进行更改。</span><span class="sxs-lookup"><span data-stu-id="287a9-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="287a9-119">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="287a9-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="287a9-120">选择**管理员**链接，然后选择**创建新**链接创建新的唱片集。</span><span class="sxs-lookup"><span data-stu-id="287a9-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="287a9-121">验证已保存的唱片集信息。</span><span class="sxs-lookup"><span data-stu-id="287a9-121">Verify the album information was saved.</span></span> <span data-ttu-id="287a9-122">编辑唱片集，并验证所做的更改会保留。</span><span class="sxs-lookup"><span data-stu-id="287a9-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="287a9-123">唱片集架构</span><span class="sxs-lookup"><span data-stu-id="287a9-123">The Album Schema</span></span>

<span data-ttu-id="287a9-124">`StoreManager`控制器创建的 MVC 基架机制允许 CRUD （创建、 读取、 更新、 删除） 访问相册中的音乐应用商店数据库。</span><span class="sxs-lookup"><span data-stu-id="287a9-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="287a9-125">唱片集信息的架构如下所示：</span><span class="sxs-lookup"><span data-stu-id="287a9-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="287a9-126">`Albums`表不存储的唱片集流派和说明，将其存储到外的键`Genres`表。</span><span class="sxs-lookup"><span data-stu-id="287a9-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="287a9-127">`Genres`表包含类型名称和说明。</span><span class="sxs-lookup"><span data-stu-id="287a9-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="287a9-128">同样，`Albums`唱片集艺术家名称，但外键的表不包含`Artists`表。</span><span class="sxs-lookup"><span data-stu-id="287a9-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="287a9-129">`Artists`表包含艺术家姓名。</span><span class="sxs-lookup"><span data-stu-id="287a9-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="287a9-130">如果您检查中的数据`Albums`表中，您可以看到每个行包含的外键`Genres`表和外键的`Artists`表。</span><span class="sxs-lookup"><span data-stu-id="287a9-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="287a9-131">下图显示从某些表数据`Albums`表。</span><span class="sxs-lookup"><span data-stu-id="287a9-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="287a9-132">HTML 选择标记</span><span class="sxs-lookup"><span data-stu-id="287a9-132">The HTML Select Tag</span></span>

<span data-ttu-id="287a9-133">HTML`<select>`元素 (由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)帮助程序) 用于显示值 （如流派列表） 的完整列表。</span><span class="sxs-lookup"><span data-stu-id="287a9-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="287a9-134">编辑窗体，当已知的当前值时，选择列表可以显示的当前值。</span><span class="sxs-lookup"><span data-stu-id="287a9-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="287a9-135">当我们将所选的值设置为此前文所示**喜剧**。</span><span class="sxs-lookup"><span data-stu-id="287a9-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="287a9-136">选择列表非常适合用于显示类别或外键数据。</span><span class="sxs-lookup"><span data-stu-id="287a9-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="287a9-137">`<select>`流派外键的元素显示可能的类型名称的列表，但保存窗体时流派属性将更新为流派外键的值，而不是显示的类型名称。</span><span class="sxs-lookup"><span data-stu-id="287a9-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="287a9-138">在下图中，是所选流派**Disco**艺术家是**Donna 夏季**。</span><span class="sxs-lookup"><span data-stu-id="287a9-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="287a9-139">检查 ASP.NET MVC 基架代码</span><span class="sxs-lookup"><span data-stu-id="287a9-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="287a9-140">打开*Controllers\StoreManagerController.cs*文件并查找`HTTP GET Create`方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="287a9-141">`Create`方法将添加两个[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)对象添加到`ViewBag`，另一个用于包含类型信息，另一个用于包含艺术家信息。</span><span class="sxs-lookup"><span data-stu-id="287a9-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="287a9-142">[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)上面使用的构造函数重载采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="287a9-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="287a9-143">*项*: [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx)包含列表中的项。</span><span class="sxs-lookup"><span data-stu-id="287a9-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="287a9-144">在上面的示例中，通过返回的流派列表`db.Genres`。</span><span class="sxs-lookup"><span data-stu-id="287a9-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="287a9-145">*dataValueField*： 在属性的名称**IEnumerable**列表，其中包含的密钥值。</span><span class="sxs-lookup"><span data-stu-id="287a9-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="287a9-146">在上述示例中，`GenreId`和`ArtistId`。</span><span class="sxs-lookup"><span data-stu-id="287a9-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="287a9-147">*dataTextField*： 在属性的名称**IEnumerable**列表，其中包含要显示的信息。</span><span class="sxs-lookup"><span data-stu-id="287a9-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="287a9-148">在艺术家和流派表`name`使用字段。</span><span class="sxs-lookup"><span data-stu-id="287a9-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="287a9-149">打开*Views\StoreManager\Create.cshtml*文件并检查`Html.DropDownList`genre 字段的帮助器标记。</span><span class="sxs-lookup"><span data-stu-id="287a9-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="287a9-150">第一行显示了创建视图，采用`Album`模型。</span><span class="sxs-lookup"><span data-stu-id="287a9-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="287a9-151">在中`Create`上面所示方法，传递没有模型，因此视图获取**null** `Album`模型。</span><span class="sxs-lookup"><span data-stu-id="287a9-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="287a9-152">此时我们将创建新的唱片集，因此我们不需要任何`Album`其数据。</span><span class="sxs-lookup"><span data-stu-id="287a9-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="287a9-153">[Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)如上所示的重载采用要绑定到模型的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="287a9-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="287a9-154">它还使用此名称来查找**ViewBag**对象，其中包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="287a9-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="287a9-155">使用此重载，将要求你将为名称**ViewBag SelectList**对象`GenreId`。</span><span class="sxs-lookup"><span data-stu-id="287a9-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="287a9-156">第二个参数 (`String.Empty`) 是当未不选定任何项时要显示的文本。</span><span class="sxs-lookup"><span data-stu-id="287a9-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="287a9-157">这正是我们想要创建新的唱片集时。</span><span class="sxs-lookup"><span data-stu-id="287a9-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="287a9-158">如果删除第二个参数，并使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="287a9-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="287a9-159">选择列表在我们的示例值默认为第一个元素或 Rock。</span><span class="sxs-lookup"><span data-stu-id="287a9-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="287a9-160">检查`HTTP POST Create`方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="287a9-161">此重载`Create`方法采用`album`创建 ASP.NET MVC 模型绑定系统从发布的表单值的对象。</span><span class="sxs-lookup"><span data-stu-id="287a9-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="287a9-162">当用户提交新的唱片集，如果模型状态无效，并且没有数据库错误时，添加新唱片集数据库。</span><span class="sxs-lookup"><span data-stu-id="287a9-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="287a9-163">下图显示了创建新的唱片集。</span><span class="sxs-lookup"><span data-stu-id="287a9-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="287a9-164">可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)若要检查的已发布的表单值的 ASP.NET MVC 模型绑定使用来创建唱片集对象。</span><span class="sxs-lookup"><span data-stu-id="287a9-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="287a9-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)。</span><span class="sxs-lookup"><span data-stu-id="287a9-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="287a9-166">重构 ViewBag SelectList 创建</span><span class="sxs-lookup"><span data-stu-id="287a9-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="287a9-167">这两个`Edit`方法和`HTTP POST Create`方法具有相同的代码来设置**SelectList**中**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="287a9-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="287a9-168">中的精神[DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself)，我们将重构此代码。</span><span class="sxs-lookup"><span data-stu-id="287a9-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="287a9-169">我们将使用此重构代码更高版本。</span><span class="sxs-lookup"><span data-stu-id="287a9-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="287a9-170">创建一个新的方法来添加流派和艺术家**SelectList**到**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="287a9-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="287a9-171">将两个行设置为`ViewBag`中的每个`Create`并`Edit`方法通过调用`SetGenreArtistViewBag`方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="287a9-172">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="287a9-173">创建新的唱片集和编辑某个唱片集以验证正常运行所做的更改。</span><span class="sxs-lookup"><span data-stu-id="287a9-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="287a9-174">显式传递到 DropDownList SelectList</span><span class="sxs-lookup"><span data-stu-id="287a9-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="287a9-175">创建和编辑视图创建的 ASP.NET MVC 基架使用以下**DropDownList**重载：</span><span class="sxs-lookup"><span data-stu-id="287a9-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="287a9-176">`DropDownList`创建视图标记，如下所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="287a9-177">因为`ViewBag`属性`SelectList`名为`GenreId`，则**DropDownList**帮助程序将使用`GenreId` **SelectList**中**ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="287a9-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="287a9-178">在下面的示例**DropDownList**重载，`SelectList`中显式传递。</span><span class="sxs-lookup"><span data-stu-id="287a9-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="287a9-179">打开*Views\StoreManager\Edit.cshtml*文件，并更改**DropDownList**调用显式传递**SelectList**，使用更高版本的重载。</span><span class="sxs-lookup"><span data-stu-id="287a9-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="287a9-180">执行此操作流派类别。</span><span class="sxs-lookup"><span data-stu-id="287a9-180">Do this for the Genre category.</span></span> <span data-ttu-id="287a9-181">已完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="287a9-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="287a9-182">运行应用程序，然后单击**管理员**链接，然后导航到 Jazz 唱片集，然后选择**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="287a9-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="287a9-183">而被显示为当前所选流派 Jazz Rock 会显示。</span><span class="sxs-lookup"><span data-stu-id="287a9-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="287a9-184">当字符串自变量 （要绑定的属性） 和**SelectList**对象具有相同的名称，则不使用所选的值。</span><span class="sxs-lookup"><span data-stu-id="287a9-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="287a9-185">浏览器时不没有提供任何所选的值，默认为中的第一个元素**SelectList**(即**Rock**在上面的示例)。</span><span class="sxs-lookup"><span data-stu-id="287a9-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="287a9-186">这是一个已知的限制**DropDownList**帮助器。</span><span class="sxs-lookup"><span data-stu-id="287a9-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="287a9-187">打开*Controllers\StoreManagerController.cs*文件，并更改**SelectList**对象名称传递给`Genres`和`Artists`。</span><span class="sxs-lookup"><span data-stu-id="287a9-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="287a9-188">已完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="287a9-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="287a9-189">流派和艺术家的名称是更好的类别的名称，因为它们包含多个只是每个类别的 ID。</span><span class="sxs-lookup"><span data-stu-id="287a9-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="287a9-190">我们之前所做的重构回报。</span><span class="sxs-lookup"><span data-stu-id="287a9-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="287a9-191">而不是更改**ViewBag**在四个方法中，我们更改被隔离到`SetGenreArtistViewBag`方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="287a9-192">更改**DropDownList**调用中创建和编辑视图，以使用新**SelectList**名称。</span><span class="sxs-lookup"><span data-stu-id="287a9-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="287a9-193">编辑视图的新标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="287a9-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="287a9-194">创建视图需要用于防止 SelectList 中的第一个项显示的空字符串。</span><span class="sxs-lookup"><span data-stu-id="287a9-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="287a9-195">创建新的唱片集和编辑某个唱片集以验证正常运行所做的更改。</span><span class="sxs-lookup"><span data-stu-id="287a9-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="287a9-196">通过选择唱片集的非 Rock genre 测试编辑代码。</span><span class="sxs-lookup"><span data-stu-id="287a9-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="287a9-197">与 DropDownList 帮助器使用视图模型</span><span class="sxs-lookup"><span data-stu-id="287a9-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="287a9-198">在名为 ViewModels 文件夹中创建一个新类`AlbumSelectListViewModel`。</span><span class="sxs-lookup"><span data-stu-id="287a9-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="287a9-199">中的代码替换为`AlbumSelectListViewModel`以下类：</span><span class="sxs-lookup"><span data-stu-id="287a9-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="287a9-200">`AlbumSelectListViewModel`构造函数采用相册、 艺术家和流派的列表，并创建一个对象，包含唱片集和一个`SelectList`流派和艺术家。</span><span class="sxs-lookup"><span data-stu-id="287a9-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="287a9-201">生成项目，因此`AlbumSelectListViewModel`当我们在下一步中创建视图时才可用。</span><span class="sxs-lookup"><span data-stu-id="287a9-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="287a9-202">添加`EditVM`方法`StoreManagerController`。</span><span class="sxs-lookup"><span data-stu-id="287a9-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="287a9-203">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="287a9-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="287a9-204">右键单击`AlbumSelectListViewModel`，选择**解决**，然后**使用 MvcMusicStore.ViewModels;**。</span><span class="sxs-lookup"><span data-stu-id="287a9-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="287a9-205">或者，可以添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="287a9-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="287a9-206">右键单击`EditVM`，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="287a9-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="287a9-207">使用如下所示的选项。</span><span class="sxs-lookup"><span data-stu-id="287a9-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="287a9-208">选择**外**，然后替换内容*Views\StoreManager\EditVM.cshtml*具有以下文件：</span><span class="sxs-lookup"><span data-stu-id="287a9-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="287a9-209">`EditVM`标记是非常类似于原始`Edit`标记有以下例外。</span><span class="sxs-lookup"><span data-stu-id="287a9-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="287a9-210">模型中的属性`Edit`视图都将窗体`model.property`(例如， `model.Title` )。</span><span class="sxs-lookup"><span data-stu-id="287a9-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="287a9-211">模型中的属性`EditVm`视图都将窗体`model.Album.property`(例如， `model.Album.Title`)。</span><span class="sxs-lookup"><span data-stu-id="287a9-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="287a9-212">这是因为`EditVM`视图为传递容器`Album`，而非`Album`如`Edit`视图。</span><span class="sxs-lookup"><span data-stu-id="287a9-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="287a9-213">**DropDownList**第二个参数来自视图模型中，不**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="287a9-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="287a9-214">**BeginForm**中的帮助程序`EditVM`视图显式回发到`Edit`操作方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="287a9-215">通过发布回`Edit`操作，我们无需编写`HTTP POST EditVM`操作并可以重复使用`HTTP POST``Edit`操作。</span><span class="sxs-lookup"><span data-stu-id="287a9-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="287a9-216">运行应用程序和编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="287a9-216">Run the application and edit an album.</span></span> <span data-ttu-id="287a9-217">更改 URL 以使用`EditVM`。</span><span class="sxs-lookup"><span data-stu-id="287a9-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="287a9-218">更改字段，然后点击**保存**按钮以验证代码是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="287a9-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="287a9-219">您应该使用哪种方法？</span><span class="sxs-lookup"><span data-stu-id="287a9-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="287a9-220">显示所有三种方法是可接受的。</span><span class="sxs-lookup"><span data-stu-id="287a9-220">All three approaches shown are acceptible.</span></span> <span data-ttu-id="287a9-221">许多开发人员更愿意使用 explictily pass`SelectList`到`DropDownList`使用`ViewBag`。</span><span class="sxs-lookup"><span data-stu-id="287a9-221">Many developers prefer to explictily pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="287a9-222">此方法具有附加的优势的让你灵活地使用找不到更合适的名称。</span><span class="sxs-lookup"><span data-stu-id="287a9-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="287a9-223">一个需要注意的是不能将命名`ViewBag SelectList`对象模型属性与相同的名称。</span><span class="sxs-lookup"><span data-stu-id="287a9-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="287a9-224">一些开发人员更喜欢 ViewModel 方法。</span><span class="sxs-lookup"><span data-stu-id="287a9-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="287a9-225">其他人考虑更冗长的标记，并生成 HTML 视图模型方法的缺点。</span><span class="sxs-lookup"><span data-stu-id="287a9-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="287a9-226">在本部分中我们已经认识到这三种方法使用**DropDownList**类别数据。</span><span class="sxs-lookup"><span data-stu-id="287a9-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="287a9-227">在下一部分中，我们将介绍如何添加新的类别。</span><span class="sxs-lookup"><span data-stu-id="287a9-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="287a9-228">[上一页](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一页](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="287a9-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
