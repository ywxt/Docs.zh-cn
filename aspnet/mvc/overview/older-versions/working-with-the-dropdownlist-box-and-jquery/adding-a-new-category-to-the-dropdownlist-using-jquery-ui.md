---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: 将新类别添加到使用 jQuery UI DropDownList |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 9fb95d22be473a4318520a391fa424106246a054
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576347"
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="3fce4-102">将新类别添加到使用 jQuery UI DropDownList</span><span class="sxs-lookup"><span data-stu-id="3fce4-102">Adding a New Category to the DropDownList using jQuery UI</span></span>
====================
<span data-ttu-id="3fce4-103">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="3fce4-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="3fce4-104">HTML`Select`标记非常适合呈现固定的类别数据列表，但通常情况下您需要添加新的类别。</span><span class="sxs-lookup"><span data-stu-id="3fce4-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="3fce4-105">假设我们想要添加到我们的数据库中的类别的流派"Opera"？</span><span class="sxs-lookup"><span data-stu-id="3fce4-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="3fce4-106">在本部分中，我们将使用的 jQuery UI 添加一个对话框，可用于添加新的类别。</span><span class="sxs-lookup"><span data-stu-id="3fce4-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="3fce4-107">下图显示了如何将用户界面显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="3fce4-108">如果用户选择**添加新流派**链接，弹出对话框中提示用户输入新的类型名称 （和可选说明）。</span><span class="sxs-lookup"><span data-stu-id="3fce4-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="3fce4-109">下面显示的图像**添加流派**弹出对话框中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="3fce4-110">当输入新的类型名称和**保存**按钮后，将发生以下事件：</span><span class="sxs-lookup"><span data-stu-id="3fce4-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="3fce4-111">AJAX 调用将数据发送到流派控制器，它将新类型保存到数据库，并返回新流派信息 （类型名称和 ID） 作为 JSON 的 Create 方法。</span><span class="sxs-lookup"><span data-stu-id="3fce4-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="3fce4-112">JavaScript 将新的类型数据添加到选择列表。</span><span class="sxs-lookup"><span data-stu-id="3fce4-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="3fce4-113">JavaScript 将新流派所选的项。</span><span class="sxs-lookup"><span data-stu-id="3fce4-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="3fce4-114">在下图**Opera**已添加到数据库和中所选**流派**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="3fce4-115">打开*Views\StoreManager\Create.cshtml*文件和流派标记替换为以下下面的代码：</span><span class="sxs-lookup"><span data-stu-id="3fce4-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="3fce4-116">`_ChooseGenre`分部视图将包含所有用于挂接的 JavaScript 和 jQuery 用于实现新添加的类型功能的逻辑。</span><span class="sxs-lookup"><span data-stu-id="3fce4-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="3fce4-117">我们完成后将可以轻松执行同样的艺术家 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="3fce4-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="3fce4-118">在解决方案资源管理器，右键单击*Views\StoreManager*文件夹，然后选择**添加**，然后**视图**。</span><span class="sxs-lookup"><span data-stu-id="3fce4-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="3fce4-119">在中**视图名称**输入、 输入`_ChooseGenre`然后选择**添加**。</span><span class="sxs-lookup"><span data-stu-id="3fce4-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="3fce4-120">替换中的标记*Views\StoreManager\\_ChooseGenre.cshtml*具有以下文件：</span><span class="sxs-lookup"><span data-stu-id="3fce4-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="3fce4-121">第一行代码声明我们传入的`Album`作为我们的模型，完全相同的模型中创建视图的语句。</span><span class="sxs-lookup"><span data-stu-id="3fce4-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="3fce4-122">接下来的几个行都**标签**帮助程序标记中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="3fce4-123">下一行是**DropDownList**帮助器调用，如下所示的原始创建视图完全相同。</span><span class="sxs-lookup"><span data-stu-id="3fce4-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="3fce4-124">下一行将具有名称的链接添加`Add New Genre`，并设置其样式类似于按钮。</span><span class="sxs-lookup"><span data-stu-id="3fce4-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="3fce4-125">行包含`ValidationMessageFor`复制直接从创建视图。</span><span class="sxs-lookup"><span data-stu-id="3fce4-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="3fce4-126">以下代码行：</span><span class="sxs-lookup"><span data-stu-id="3fce4-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="3fce4-127">创建隐藏的 div，id 为`genreDialog`。</span><span class="sxs-lookup"><span data-stu-id="3fce4-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="3fce4-128">我们将使用 jQuery 来挂接我们**添加流派**对话框中的 id`genreDialog`中此 div。</span><span class="sxs-lookup"><span data-stu-id="3fce4-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="3fce4-129">最后两个脚本标记包含我们将使用为实现添加的新流派功能的 JavaScript 文件的链接。</span><span class="sxs-lookup"><span data-stu-id="3fce4-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="3fce4-130">*/Scripts/chooseGenre.js*文件是提供有关你的项目中，我们将检查它本教程的后面。</span><span class="sxs-lookup"><span data-stu-id="3fce4-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="3fce4-131">运行应用程序并单击**添加新流派**按钮。</span><span class="sxs-lookup"><span data-stu-id="3fce4-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="3fce4-132">在中**添加流派**对话框框中，输入**Opera**中**名称**输入的框。</span><span class="sxs-lookup"><span data-stu-id="3fce4-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="3fce4-133">单击“保存”按钮。</span><span class="sxs-lookup"><span data-stu-id="3fce4-133">Click the **Save** button.</span></span> <span data-ttu-id="3fce4-134">AJAX 调用创建 Opera 类别然后填充 Opera，下拉列表并设置为所选流派 Opera。</span><span class="sxs-lookup"><span data-stu-id="3fce4-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="3fce4-135">输入艺术家、 标题和价格，然后选择**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="3fce4-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="3fce4-136">如果输入小于 8.99 美元的价格，新的唱片集将出现在索引视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="3fce4-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="3fce4-137">验证新的唱片集条目已保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="3fce4-138">尝试使用只有一个字母创建的新流派。</span><span class="sxs-lookup"><span data-stu-id="3fce4-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="3fce4-139">下面的代码中*Models\Genre.cs*文件设置的类型名称的最小值和最大长度。</span><span class="sxs-lookup"><span data-stu-id="3fce4-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="3fce4-140">客户端验证报告必须输入介于 2 到 20 个字符之间的字符串。</span><span class="sxs-lookup"><span data-stu-id="3fce4-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="3fce4-141">检查如何新类型添加到数据库和选择列表中。</span><span class="sxs-lookup"><span data-stu-id="3fce4-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="3fce4-142">打开*Scripts\chooseGenre.js*文件并检查代码。</span><span class="sxs-lookup"><span data-stu-id="3fce4-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="3fce4-143">第二行使用 ID`genreDialog`上的 div 标记中创建一个对话框*Views\StoreManager\\_ChooseGenre.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="3fce4-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="3fce4-144">命名参数的大多数都是自解释性。</span><span class="sxs-lookup"><span data-stu-id="3fce4-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="3fce4-145">`autoOpen`参数设置为 false，选择**创建流派**按钮将显式打开对话框 （这介绍后一种上）。</span><span class="sxs-lookup"><span data-stu-id="3fce4-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="3fce4-146">对话框有两个按钮**保存**并**取消**。</span><span class="sxs-lookup"><span data-stu-id="3fce4-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="3fce4-147">**取消**按钮关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="3fce4-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="3fce4-148">下面的代码演示**保存**按钮函数。</span><span class="sxs-lookup"><span data-stu-id="3fce4-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="3fce4-149">`var createGenreForm`从所选`createGenreForm`id。</span><span class="sxs-lookup"><span data-stu-id="3fce4-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="3fce4-150">`createGenreForm` ID 已在中的以下代码中设置*Views\Genre\\_CreateGenre.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="3fce4-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="3fce4-151">[Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx)中使用的帮助程序重载*Views\Genre\\_CreateGenre.cshtml*文件的操作属性包含要提交窗体的 URL 生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="3fce4-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="3fce4-152">您可以看到这通过在浏览器中显示创建唱片集页并在浏览器中选择显示源。</span><span class="sxs-lookup"><span data-stu-id="3fce4-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="3fce4-153">以下标记显示了生成包含窗体标记的 HTML。</span><span class="sxs-lookup"><span data-stu-id="3fce4-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="3fce4-154">JQuery`$.post`行进行 AJAX 调用到操作属性 (`/StoreManager/Create`)，并将从数据中传递**创建流派**对话框。</span><span class="sxs-lookup"><span data-stu-id="3fce4-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="3fce4-155">数据包含的名称的新流派和可选描述。</span><span class="sxs-lookup"><span data-stu-id="3fce4-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="3fce4-156">如果 AJAX 调用成功，新类型名称和值添加到选择的标记和新流派设置为所选的值。</span><span class="sxs-lookup"><span data-stu-id="3fce4-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="3fce4-157">由于这是动态生成的标记，通过在浏览器中查看源，不能看到新选择的选项。</span><span class="sxs-lookup"><span data-stu-id="3fce4-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="3fce4-158">可以看到与 IE 9 F12 开发人员工具的新 HTML。</span><span class="sxs-lookup"><span data-stu-id="3fce4-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="3fce4-159">要在 Internet Explorer 9 中查看新选择的选项，请按 F12 键以启动 F12 开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="3fce4-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="3fce4-160">导航到创建页，并添加新流派，以便在流派选择列表中选择新流派。</span><span class="sxs-lookup"><span data-stu-id="3fce4-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="3fce4-161">中的 F12 开发人员工具：</span><span class="sxs-lookup"><span data-stu-id="3fce4-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="3fce4-162">选择 HTML 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3fce4-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="3fce4-163">按刷新图标。</span><span class="sxs-lookup"><span data-stu-id="3fce4-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="3fce4-164">在搜索框中，输入 GenreID。</span><span class="sxs-lookup"><span data-stu-id="3fce4-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="3fce4-165">使用下一步图标，</span><span class="sxs-lookup"><span data-stu-id="3fce4-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="3fce4-166">导航到以下 select 标记：</span><span class="sxs-lookup"><span data-stu-id="3fce4-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="3fce4-167">展开的最后一个选项值。</span><span class="sxs-lookup"><span data-stu-id="3fce4-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="3fce4-168">下面的代码中*Scripts\chooseGenre.js*文件演示如何**添加新流派**按钮获取连接到了 click 事件，以及如何**添加新流派**对话框创建。</span><span class="sxs-lookup"><span data-stu-id="3fce4-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="3fce4-169">第一行创建附加到的单击函数**添加新流派**按钮。</span><span class="sxs-lookup"><span data-stu-id="3fce4-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="3fce4-170">以下标记从 Views\StoreManager\\_ChooseGenre.cshtml 文件显示了如何**添加新流派**创建按钮：</span><span class="sxs-lookup"><span data-stu-id="3fce4-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="3fce4-171">Load 方法创建和打开添加类型对话框并调用 jQuery`parse`方法，以便在对话框中输入的数据时执行客户端验证。</span><span class="sxs-lookup"><span data-stu-id="3fce4-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="3fce4-172">在本部分介绍了如何创建一个对话框，可用于将新类别数据添加到选择列表。</span><span class="sxs-lookup"><span data-stu-id="3fce4-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="3fce4-173">可以按照相同的过程来创建用于向艺术家选择列表中添加新的艺术家 UI。</span><span class="sxs-lookup"><span data-stu-id="3fce4-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="3fce4-174">本教程提供的使用 ASP.NET MVC HTML 帮助器概述**DropDownList**。</span><span class="sxs-lookup"><span data-stu-id="3fce4-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="3fce4-175">有关使用的其他信息**DropDownList**，请参阅添加引用部分下。</span><span class="sxs-lookup"><span data-stu-id="3fce4-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="3fce4-176">请让我们知道是否本教程中对你有所帮助。</span><span class="sxs-lookup"><span data-stu-id="3fce4-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="3fce4-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3fce4-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="3fce4-178">其他参考</span><span class="sxs-lookup"><span data-stu-id="3fce4-178">Additional References</span></span>

- <span data-ttu-id="3fce4-179">[ASP.NET MVC – 级联下拉列表中列出了教程](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx)通过[Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="3fce4-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="3fce4-180">[所选](http://harvesthq.github.com/chosen/)JavaScript 插件，支持多选和筛选。</span><span class="sxs-lookup"><span data-stu-id="3fce4-180">[Chosen](http://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="3fce4-181">参与者</span><span class="sxs-lookup"><span data-stu-id="3fce4-181">Contributors</span></span>

- [<span data-ttu-id="3fce4-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="3fce4-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="3fce4-183">Jean Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="3fce4-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="3fce4-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="3fce4-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="3fce4-185">审阅者</span><span class="sxs-lookup"><span data-stu-id="3fce4-185">Reviewers</span></span>

- <span data-ttu-id="3fce4-186">Jean Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="3fce4-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="3fce4-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="3fce4-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="3fce4-188">Mike 教皇</span><span class="sxs-lookup"><span data-stu-id="3fce4-188">Mike Pope</span></span>
- <span data-ttu-id="3fce4-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="3fce4-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3fce4-190">上一篇</span><span class="sxs-lookup"><span data-stu-id="3fce4-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
