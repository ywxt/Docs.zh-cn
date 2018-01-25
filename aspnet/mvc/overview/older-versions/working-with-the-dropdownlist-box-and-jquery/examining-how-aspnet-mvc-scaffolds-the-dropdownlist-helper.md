---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: "检查如何 ASP.NET MVC scaffolds DropDownList 帮助器 |Microsoft 文档"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 737773ab424b3ec3b6139b8c238a60ca23de2e69
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="2e9f0-102">检查如何 ASP.NET MVC scaffolds DropDownList 帮助器</span><span class="sxs-lookup"><span data-stu-id="2e9f0-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>
====================
<span data-ttu-id="2e9f0-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="2e9f0-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="2e9f0-104">在**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="2e9f0-105">控制器**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="2e9f0-106">设置选项**添加控制器**下图中所示的对话框。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="2e9f0-107">编辑*StoreManager\Index.cshtml*查看和删除`AlbumArtUrl`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="2e9f0-108">删除`AlbumArtUrl`将使演示文稿更具可读性。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="2e9f0-109">已完成的代码所示。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="2e9f0-110">打开*Controllers\StoreManagerController.cs*文件并查找`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="2e9f0-111">添加`OrderBy`子句，以便唱片集将按价格进行排序。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="2e9f0-112">完整的代码所示。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="2e9f0-113">价格按排序将使其可以轻松地测试对数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="2e9f0-114">当你要测试的编辑，并创建方法时，可以使用较低成本，因此将第一个显示保存的数据。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="2e9f0-115">打开*StoreManager\Edit.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="2e9f0-116">图例标记的后面添加以下行。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="2e9f0-117">下面的代码演示此更改的上下文：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="2e9f0-118">`AlbumId`需对唱片集记录进行更改。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="2e9f0-119">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="2e9f0-120">选择**管理员**链接，然后选择**新建**链接创建新唱片集。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="2e9f0-121">验证已保存的唱片集信息。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-121">Verify the album information was saved.</span></span> <span data-ttu-id="2e9f0-122">编辑唱片集并验证你所做的更改将保留。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="2e9f0-123">唱片集架构</span><span class="sxs-lookup"><span data-stu-id="2e9f0-123">The Album Schema</span></span>

<span data-ttu-id="2e9f0-124">`StoreManager`控制器创建的 MVC 基架机制允许专辑 CRUD （创建、 读取、 更新、 删除） 访问音乐存储数据库中。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="2e9f0-125">唱片集信息的架构如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="2e9f0-126">`Albums`表不会存储唱片集 genre 和描述，它将存储的外键`Genres`表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="2e9f0-127">`Genres`表包含的流派名称和描述。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="2e9f0-128">同样，`Albums`表不包含唱片集艺术家名称，但外的键与`Artists`表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="2e9f0-129">`Artists`表包含艺术家的名称。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="2e9f0-130">如果检查中的数据`Albums`表，你可以看到每一行都包含外的键与`Genres`表和外的键与`Artists`表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="2e9f0-131">下图显示的某些表数据来自`Albums`表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="2e9f0-132">HTML 选择标记</span><span class="sxs-lookup"><span data-stu-id="2e9f0-132">The HTML Select Tag</span></span>

<span data-ttu-id="2e9f0-133">HTML`<select>`元素 (由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)帮助程序) 用于显示值 （如风格的列表） 的完整列表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="2e9f0-134">对于编辑窗体中，当已知的当前值时，选择列表可以显示的当前值。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="2e9f0-135">我们已了解此以前当我们设置为所选的值**喜剧**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="2e9f0-136">选择列表非常适合于显示类别或外键数据。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="2e9f0-137">`<select>`流派外键的元素显示名称的列表可能流派，但时保存该窗体流派属性将更新为流派外键值，而不是显示的流派名称。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="2e9f0-138">在下图中，选择流派是**Disco**艺术家且**Donna 夏天**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="2e9f0-139">检查 ASP.NET MVC 基架代码</span><span class="sxs-lookup"><span data-stu-id="2e9f0-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="2e9f0-140">打开*Controllers\StoreManagerController.cs*文件并查找`HTTP GET Create`方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="2e9f0-141">`Create`方法添加两个[此时](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)对象添加到`ViewBag`，另一个用于包含流派信息，另一个用于包含艺术家信息。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="2e9f0-142">[此时](https://msdn.microsoft.com/library/dd505286.aspx)上面使用的构造函数重载采用三个自变量：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="2e9f0-143">*项*: [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx)包含列表中的项。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="2e9f0-144">在上面的示例中，返回的风格列表`db.Genres`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="2e9f0-145">*dataValueField*： 中的属性的名称**IEnumerable**包含密钥的值的列表。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="2e9f0-146">在上例中，`GenreId`和`ArtistId`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="2e9f0-147">*dataTextField*： 中的属性的名称**IEnumerable**列表，其中包含要显示的信息。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="2e9f0-148">在专业人员和风格表`name`使用字段。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="2e9f0-149">打开*Views\StoreManager\Create.cshtml*文件并检查`Html.DropDownList`genre 字段的帮助器标记。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="2e9f0-150">第一行显示创建视图所`Album`模型。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="2e9f0-151">在`Create`上面所示方法，不传递任何模型，因此视图获取**null** `Album`模型。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="2e9f0-152">此时我们将创建新唱片集，因此我们没有任何`Album`为它的数据。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="2e9f0-153">[Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)上面所示的重载采用要绑定到模型的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="2e9f0-154">它还使用此名称来查找**ViewBag**对象，其中包含[此时](https://msdn.microsoft.com/library/dd505286.aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="2e9f0-155">使用此重载，将要求你将为名称**ViewBag 此时**对象`GenreId`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="2e9f0-156">第二个参数 (`String.Empty`) 是要在未不选定任何项时显示的文本。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="2e9f0-157">这正是我们想要创建新唱片集时。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="2e9f0-158">如果你删除第二个参数，并使用下面的代码：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="2e9f0-159">在我们的示例情况下，选择列表将默认为第一个元素或 Rock。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="2e9f0-160">检查`HTTP POST Create`方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="2e9f0-161">此重载`Create`方法采用`album`创建 ASP.NET MVC 模型绑定系统从窗体值发布的对象。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="2e9f0-162">当你提交新唱片集，模型状态有效并且没有数据库错误时，将数据库被添加新唱片集。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="2e9f0-163">下图显示新唱片集的创建。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="2e9f0-164">你可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)检查已发布的窗体值绑定的 ASP.NET MVC 模型使用来创建唱片集对象。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="2e9f0-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="2e9f0-166">重构 ViewBag 此时创建</span><span class="sxs-lookup"><span data-stu-id="2e9f0-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="2e9f0-167">这两个`Edit`方法和`HTTP POST Create`方法具有相同的代码，若要设置**此时**中**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="2e9f0-168">中的设计理念[干](http://en.wikipedia.org/wiki/Don't_repeat_yourself)，我们将重构此代码。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="2e9f0-169">我们将使此使用重构代码更高版本。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="2e9f0-170">创建一个新方法以便添加 genre 和艺术家**此时**到**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="2e9f0-171">将两个行设置`ViewBag`中每个`Create`和`Edit`方法通过调用`SetGenreArtistViewBag`方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="2e9f0-172">已完成的代码所示。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="2e9f0-173">创建新唱片集和编辑唱片集以验证更改正常。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="2e9f0-174">显式将此时传递到下拉列表</span><span class="sxs-lookup"><span data-stu-id="2e9f0-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="2e9f0-175">创建和编辑视图创建的 ASP.NET MVC 基架使用以下**DropDownList**重载：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="2e9f0-176">`DropDownList`创建视图标记，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="2e9f0-177">因为`ViewBag`属性`SelectList`名为`GenreId`、 **DropDownList**帮助程序将使用`GenreId`**此时**中**ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="2e9f0-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="2e9f0-178">在下面的示例**DropDownList**超负荷运转，`SelectList`显式传递中。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="2e9f0-179">打开*Views\StoreManager\Edit.cshtml*文件，并将更改**DropDownList**调用中显式传递**此时**，使用上面的重载。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="2e9f0-180">执行此操作为流派类别。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-180">Do this for the Genre category.</span></span> <span data-ttu-id="2e9f0-181">已完成的代码所示：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="2e9f0-182">运行应用程序，然后单击**管理员**链接，然后导航到爵士乐唱片集并选择**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="2e9f0-183">而不被显示为当前所选风格爵士乐，将显示 Rock。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="2e9f0-184">当字符串参数 （要绑定的属性） 和**此时**对象具有相同的名称，则不会使用所选的值。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="2e9f0-185">中的第一个元素时没有提供所选的值，默认浏览器**此时**(即**Rock**在上面的示例)。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="2e9f0-186">这是已知的限制**DropDownList**帮助器。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="2e9f0-187">打开*Controllers\StoreManagerController.cs*文件并将更改**此时**对象名称传递给`Genres`和`Artists`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="2e9f0-188">已完成的代码所示：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="2e9f0-189">风格和艺术家更好名称是为类别，因为它们具有以外的其他每个类别的 ID。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="2e9f0-190">重构我们此前回报。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="2e9f0-191">而不是更改**ViewBag**在四个方法中，我们更改了隔离到`SetGenreArtistViewBag`方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="2e9f0-192">更改**DropDownList**调用在创建和编辑视图以使用新**此时**名称。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="2e9f0-193">编辑视图的新标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="2e9f0-194">创建视图需要一个空字符串，以防止显示此时的第一项。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="2e9f0-195">创建新唱片集和编辑唱片集以验证更改正常。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="2e9f0-196">通过选择与以外 Rock 流派唱片集测试编辑代码。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="2e9f0-197">使用视图模型具有 DropDownList 帮助程序</span><span class="sxs-lookup"><span data-stu-id="2e9f0-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="2e9f0-198">名为的 Viewmodel 文件夹中创建一个新类`AlbumSelectListViewModel`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="2e9f0-199">中的代码替换`AlbumSelectListViewModel`替换为以下类：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="2e9f0-200">`AlbumSelectListViewModel`构造函数采用唱片集、 专业人员和风格的列表，并创建一个包含唱片集的对象和一个`SelectList`风格和艺术家。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="2e9f0-201">生成项目因此`AlbumSelectListViewModel`当我们在下一步中创建视图时才可用。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="2e9f0-202">添加`EditVM`方法`StoreManagerController`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="2e9f0-203">已完成的代码所示。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="2e9f0-204">右键单击`AlbumSelectListViewModel`，选择**解决**，然后**使用 MvcMusicStore.ViewModels;**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="2e9f0-205">或者，可以添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="2e9f0-206">右键单击`EditVM`和选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="2e9f0-207">使用下面所示的选项。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="2e9f0-208">选择**添加**，然后替换内容*Views\StoreManager\EditVM.cshtml*替换为以下文件：</span><span class="sxs-lookup"><span data-stu-id="2e9f0-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="2e9f0-209">`EditVM`标记是非常类似于原始`Edit`标记有以下例外。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="2e9f0-210">模型中的属性`Edit`视图是在窗体`model.property`(例如， `model.Title` )。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="2e9f0-211">模型中的属性`EditVm`视图是在窗体`model.Album.property`(例如， `model.Album.Title`)。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="2e9f0-212">这是因为`EditVM`视图为传递容器`Album`，而不`Album`作为 in`Edit`视图。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="2e9f0-213">**DropDownList**第二个参数不是来自视图模型， **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="2e9f0-214">**BeginForm**中的帮助器`EditVM`视图显式回发到`Edit`操作方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="2e9f0-215">通过发布回`Edit`操作，我们不需要编写`HTTP POST EditVM`操作并可以重用`HTTP POST``Edit`操作。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="2e9f0-216">运行应用程序和编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-216">Run the application and edit an album.</span></span> <span data-ttu-id="2e9f0-217">将 URL 更改为使用`EditVM`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="2e9f0-218">更改的字段，并按**保存**按钮来验证代码能够工作。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="2e9f0-219">你应使用哪种方法？</span><span class="sxs-lookup"><span data-stu-id="2e9f0-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="2e9f0-220">显示的所有三种方法是可接受的。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-220">All three approaches shown are acceptible.</span></span> <span data-ttu-id="2e9f0-221">许多开发人员更愿意使用 explictily 传递`SelectList`到`DropDownList`使用`ViewBag`。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-221">Many developers prefer to explictily pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="2e9f0-222">此方法的优点添加了为您提供使用找不到更合适的名称的灵活性。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="2e9f0-223">一个需要注意的是不能将命名`ViewBag SelectList`对象模型属性与相同的名称。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="2e9f0-224">一些开发人员更喜欢 ViewModel 方法。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="2e9f0-225">其他请考虑更详细标记和视图模型已生成的 HTML 接近缺点。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-225">Others consider the the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="2e9f0-226">在本部分中我们已了解到使用的三种方法**DropDownList**类别数据。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="2e9f0-227">在下一步的部分中，我们将展示如何添加新类别。</span><span class="sxs-lookup"><span data-stu-id="2e9f0-227">In the next section, we'll show how to add a new category.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2e9f0-228">[上一页](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[下一页](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="2e9f0-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
