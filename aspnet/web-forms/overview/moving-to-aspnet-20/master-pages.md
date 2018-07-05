---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |Microsoft Docs
author: microsoft
description: 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员用于用户控件复制常见页 elem....
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b31627fec45f153f5832afa6e317f2dd2b296d02
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382616"
---
<a name="master-pages"></a><span data-ttu-id="20947-104">母版页</span><span class="sxs-lookup"><span data-stu-id="20947-104">Master Pages</span></span>
====================
<span data-ttu-id="20947-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="20947-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="20947-106">成功的网站的关键组件之一是一致的外观。</span><span class="sxs-lookup"><span data-stu-id="20947-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="20947-107">在 ASP.NET 1.x 中，开发人员使用用户控件在 Web 应用程序之间复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="20947-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="20947-108">虽然这的确是一个可行的解决方案，则使用用户控件也有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="20947-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="20947-109">例如，用户控件的位置的更改在站点之间要求对多个页面的更改。</span><span class="sxs-lookup"><span data-stu-id="20947-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="20947-110">用户控件也不会呈现在页面上插入后的设计视图中。</span><span class="sxs-lookup"><span data-stu-id="20947-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>


<span data-ttu-id="20947-111">成功的网站的关键组件之一是一致的外观。</span><span class="sxs-lookup"><span data-stu-id="20947-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="20947-112">在 ASP.NET 1.x 中，开发人员使用用户控件在 Web 应用程序之间复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="20947-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="20947-113">虽然这的确是一个可行的解决方案，则使用用户控件也有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="20947-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="20947-114">例如，用户控件的位置的更改在站点之间要求对多个页面的更改。</span><span class="sxs-lookup"><span data-stu-id="20947-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="20947-115">用户控件也不会呈现在页面上插入后的设计视图中。</span><span class="sxs-lookup"><span data-stu-id="20947-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="20947-116">ASP.NET 2.0 引入了 Master 页作为维护一致的外观和感觉，一种方式以及您一会儿将看到，主页面表示用户控件方法上的一个显著的改进。</span><span class="sxs-lookup"><span data-stu-id="20947-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="20947-117">为什么主页？</span><span class="sxs-lookup"><span data-stu-id="20947-117">Why Master Pages?</span></span>

<span data-ttu-id="20947-118">你可能想知道为什么主页面 ASP.NET 2.0 中需要。</span><span class="sxs-lookup"><span data-stu-id="20947-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="20947-119">毕竟，网站开发人员已在使用用户控件在 ASP.NET 1.x 共享页之间的内容区域。</span><span class="sxs-lookup"><span data-stu-id="20947-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="20947-120">实际原因有多种原因用户控件都是不太理想的解决方案，用于创建一个通用布局。</span><span class="sxs-lookup"><span data-stu-id="20947-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="20947-121">用户控件实际上不定义页面布局。</span><span class="sxs-lookup"><span data-stu-id="20947-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="20947-122">相反，它们定义的布局和页面的一个部分的功能。</span><span class="sxs-lookup"><span data-stu-id="20947-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="20947-123">这两者之间的差异非常重要，因为它使用户控制解决方案的可管理性要困难得多。</span><span class="sxs-lookup"><span data-stu-id="20947-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="20947-124">例如，当你想要更改您的页面上的用户控件的位置，必须编辑用户控件显示的实际页。</span><span class="sxs-lookup"><span data-stu-id="20947-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="20947-125">如果你有仅几个页面，但在大型站点中，它很快会变得站点管理噩梦，这会精确地 ！</span><span class="sxs-lookup"><span data-stu-id="20947-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="20947-126">使用用户控件，用于定义一个通用布局的另一个缺点是在 ASP.NET 中的体系结构中取得 root 权限。</span><span class="sxs-lookup"><span data-stu-id="20947-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="20947-127">如果更改用户控件的任何公共成员，它要求您重新编译所有页面，使用用户控件。</span><span class="sxs-lookup"><span data-stu-id="20947-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="20947-128">反过来，ASP.NET 将然后 re JIT 页面首次访问。</span><span class="sxs-lookup"><span data-stu-id="20947-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="20947-129">此操作，请再次重申，生成一个非可缩放的体系结构以及较大的站点的站点管理问题。</span><span class="sxs-lookup"><span data-stu-id="20947-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="20947-130">在 ASP.NET 2.0 中的主页面可以很好地解决这些问题 （和更多）。</span><span class="sxs-lookup"><span data-stu-id="20947-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="20947-131">如何母版页的工作原理</span><span class="sxs-lookup"><span data-stu-id="20947-131">How Master Pages Work</span></span>

<span data-ttu-id="20947-132">母版页是类似于其他页面的模板。</span><span class="sxs-lookup"><span data-stu-id="20947-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="20947-133">应在其他页面 （即菜单、 边框等） 之间共享的页面元素添加到母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="20947-134">当新页面添加到该站点时，可以将其关联与母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="20947-135">调用页与母版页相关联**内容页**。</span><span class="sxs-lookup"><span data-stu-id="20947-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="20947-136">默认情况下，内容页面采用从母版页的外观。</span><span class="sxs-lookup"><span data-stu-id="20947-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="20947-137">但是，当创建主页面，可以定义内容页可以将其自己的内容替换为页面的部分。</span><span class="sxs-lookup"><span data-stu-id="20947-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="20947-138">这些部分都是使用 ASP.NET 2.0; 中引入的新控件定义**ContentPlaceHolder**控件。</span><span class="sxs-lookup"><span data-stu-id="20947-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="20947-139">主页面可以包含任意数量的 ContentPlaceHolder 控件 （或根本未。）在内容页上从 ContentPlaceHolder 控件内容的显示的内部**内容**控件、 ASP.NET 2.0 中的另一个新控件。</span><span class="sxs-lookup"><span data-stu-id="20947-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="20947-140">默认情况下，内容控件的内容页是空的以便可以提供自己的内容。</span><span class="sxs-lookup"><span data-stu-id="20947-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="20947-141">如果你想要使用内容控件在母版页中的内容，则可以执行将看到更高版本在此模块中。</span><span class="sxs-lookup"><span data-stu-id="20947-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="20947-142">内容控件映射到内容控件的 ContentPlaceHolderID 特性通过 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="20947-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="20947-143">以下映射代码到 ContentPlaceHolder 控件在母版页上调用 mainBody 内容控件。</span><span class="sxs-lookup"><span data-stu-id="20947-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="20947-144">您将经常听人们描述为基类的其他页面的母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="20947-145">这是实际不适用。</span><span class="sxs-lookup"><span data-stu-id="20947-145">Thats actually not true.</span></span> <span data-ttu-id="20947-146">母版页和内容页之间的关系不是继承。</span><span class="sxs-lookup"><span data-stu-id="20947-146">The relationship between master pages and content pages is not one of inheritance.</span></span>


<span data-ttu-id="20947-147">**图 1**显示主控页和关联的内容页中 Visual Studio 2005 的显示方式。</span><span class="sxs-lookup"><span data-stu-id="20947-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="20947-148">可以看到在母版页和相应的 ContentPlaceHolder 控件内容的内容页中的控件。</span><span class="sxs-lookup"><span data-stu-id="20947-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="20947-149">请注意，外部 ContentPlaceHolder 的主页面内容可见，但在内容页中灰显。</span><span class="sxs-lookup"><span data-stu-id="20947-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="20947-150">仅将 ContentPlaceHolder 内的内容可以通过内容页所取代。</span><span class="sxs-lookup"><span data-stu-id="20947-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="20947-151">所有其他来自母版页的内容是不可变。</span><span class="sxs-lookup"><span data-stu-id="20947-151">All other content that comes from the master page is immutable.</span></span>


![母版页和其关联的内容页](master-pages/_static/image1.jpg)

<span data-ttu-id="20947-153">**图 1**： 主控页和其关联的内容页</span><span class="sxs-lookup"><span data-stu-id="20947-153">**Figure 1**: A master page and its associated content page</span></span>


## <a name="creating-a-master-page"></a><span data-ttu-id="20947-154">创建主页面</span><span class="sxs-lookup"><span data-stu-id="20947-154">Creating a Master Page</span></span>

<span data-ttu-id="20947-155">若要创建新的主页面：</span><span class="sxs-lookup"><span data-stu-id="20947-155">To create a new master page:</span></span>

1. <span data-ttu-id="20947-156">打开 Visual Studio 2005 并创建新的 Web 站点。</span><span class="sxs-lookup"><span data-stu-id="20947-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="20947-157">单击文件，新、 文件。</span><span class="sxs-lookup"><span data-stu-id="20947-157">Click File, New, File.</span></span>
3. <span data-ttu-id="20947-158">从添加新项对话框中选择主文件，如中所示**图 2**。</span><span class="sxs-lookup"><span data-stu-id="20947-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="20947-159">单击添加。</span><span class="sxs-lookup"><span data-stu-id="20947-159">Click Add.</span></span>


![创建一个新的主页面](master-pages/_static/image2.jpg)

<span data-ttu-id="20947-161">**图 2**： 创建新的主页面</span><span class="sxs-lookup"><span data-stu-id="20947-161">**Figure 2**: Creating a New Master Page</span></span>


<span data-ttu-id="20947-162">请注意，文件扩展名为母版页<em>.master</em>。</span><span class="sxs-lookup"><span data-stu-id="20947-162">Notice that the file extension for a master page is <em>.master</em>.</span></span> <span data-ttu-id="20947-163">这是主页面与普通页不同的方法之一。</span><span class="sxs-lookup"><span data-stu-id="20947-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="20947-164">其他主要区别是替代@Page指令，母版页包含@Master指令。</span><span class="sxs-lookup"><span data-stu-id="20947-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="20947-165">切换到源视图的主页面，刚刚创建并查看代码。</span><span class="sxs-lookup"><span data-stu-id="20947-165">Switch to Source View for the master page youve just created and review the code.</span></span>

<span data-ttu-id="20947-166">默认情况下，新的主页面将具有一个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="20947-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="20947-167">在大多数情况下，它更有意义可以首先创建常见的页面元素然后插入 ContentPlaceHolder 控件在需要自定义内容的情况。</span><span class="sxs-lookup"><span data-stu-id="20947-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="20947-168">在这些情况下，开发人员将想要删除默认 ContentPlaceHolder 控件并插入新的开发页。</span><span class="sxs-lookup"><span data-stu-id="20947-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="20947-169">ContentPlaceHolder 控件不能调整大小，它们显示调整大小控点的情况。</span><span class="sxs-lookup"><span data-stu-id="20947-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="20947-170">自动根据它包含有一个例外; 的内容的 ContentPlaceHolder 控件大小如果如表格单元格将 ContentPlaceHolder 控件在是块元素内部，它将根据元素的大小调整大小。</span><span class="sxs-lookup"><span data-stu-id="20947-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="20947-171">实验室 1 使用母版页</span><span class="sxs-lookup"><span data-stu-id="20947-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="20947-172">在此实验中，将创建新的主页面，并定义三个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="20947-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="20947-173">然后，将创建新的内容页面，并替换为从至少其中一个 ContentPlaceHolder 控件的内容。</span><span class="sxs-lookup"><span data-stu-id="20947-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="20947-174">创建主页面，并插入 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="20947-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="20947-175">创建新的主页面，如上文所述。</span><span class="sxs-lookup"><span data-stu-id="20947-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="20947-176">删除默认 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="20947-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="20947-177">通过单击该控件的阴影上边框选择 ContentPlaceHolder 控件，然后按你键盘上的 DEL 键中删除它。</span><span class="sxs-lookup"><span data-stu-id="20947-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="20947-178">插入新表使用*标头和端*图 3 中所示的模板。</span><span class="sxs-lookup"><span data-stu-id="20947-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="20947-179">将宽度和高度更改为 90%，以使整个表设计器中可见。</span><span class="sxs-lookup"><span data-stu-id="20947-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>


![](master-pages/_static/image3.jpg)

<span data-ttu-id="20947-180">**图 3**</span><span class="sxs-lookup"><span data-stu-id="20947-180">**Figure 3**</span></span>


1. <span data-ttu-id="20947-181">将光标置于表的每个单元格并设置*valign*属性设置为*顶部*。</span><span class="sxs-lookup"><span data-stu-id="20947-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="20947-182">从工具箱中的表 （的标头单元格。） 的顶部单元插入 ContentPlaceHolder 控件</span><span class="sxs-lookup"><span data-stu-id="20947-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="20947-183">当插入此 ContentPlaceHolder 控件时，您会注意到行的高度将几乎整个页面占用，如图 4 中所示。</span><span class="sxs-lookup"><span data-stu-id="20947-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="20947-184">不能胜，此时。</span><span class="sxs-lookup"><span data-stu-id="20947-184">Dont be concerned about that at this point.</span></span>


![作为 ContentPlaceHolder 相同单元中是空的空间](master-pages/_static/image1.gif)

<span data-ttu-id="20947-186">**图 4**: ContentPlaceHolder 格中是空的空间</span><span class="sxs-lookup"><span data-stu-id="20947-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>


1. <span data-ttu-id="20947-187">将 ContentPlaceHolder 控件放在其他两个单元格。</span><span class="sxs-lookup"><span data-stu-id="20947-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="20947-188">一旦已插入其他 ContentPlaceHolder 控件，表格单元格的大小应为按预期的方式。</span><span class="sxs-lookup"><span data-stu-id="20947-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="20947-189">页面现在应如下所示中显示的页面**图 5**。</span><span class="sxs-lookup"><span data-stu-id="20947-189">The page should now look like the page shown in **figure 5**.</span></span>


![与所有 ContentPlaceHolder 控件 Master。](master-pages/_static/image2.gif)

<span data-ttu-id="20947-192">**图 5**： 与所有 ContentPlaceHolder 控件的母版。</span><span class="sxs-lookup"><span data-stu-id="20947-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="20947-193">请注意，标头单元格的单元格高度现在它应该是什么</span><span class="sxs-lookup"><span data-stu-id="20947-193">Notice that the cell height for the header cell is now what it should be</span></span>


1. <span data-ttu-id="20947-194">每三个 ContentPlaceHolder 控件中输入所选的某些文本。</span><span class="sxs-lookup"><span data-stu-id="20947-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="20947-195">将为 exercise1.master 母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="20947-196">创建新的 Web 窗体并将其与 exercise1.master 母版页相关联。</span><span class="sxs-lookup"><span data-stu-id="20947-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="20947-197">选择新建文件、 文件在 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="20947-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="20947-198">选择**Web 窗体**在添加新项对话框。</span><span class="sxs-lookup"><span data-stu-id="20947-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="20947-199">请确保选中选择母版页复选框，如图 6 中所示。</span><span class="sxs-lookup"><span data-stu-id="20947-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>


![添加一个新的内容页](master-pages/_static/image3.gif)

<span data-ttu-id="20947-201">**图 6**： 添加新的内容页面</span><span class="sxs-lookup"><span data-stu-id="20947-201">**Figure 6**: Adding a new Content Page</span></span>


1. <span data-ttu-id="20947-202">单击添加。</span><span class="sxs-lookup"><span data-stu-id="20947-202">Click Add.</span></span>
2. <span data-ttu-id="20947-203">选择 exercise1.master 在中，选择一个母版页对话框图 7 中所示。</span><span class="sxs-lookup"><span data-stu-id="20947-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="20947-204">单击确定以添加新的内容页面。</span><span class="sxs-lookup"><span data-stu-id="20947-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="20947-205">新的内容页出现在 Visual Studio 为每个 ContentPlaceHolder 控件在母版页上的其中一个内容控件。</span><span class="sxs-lookup"><span data-stu-id="20947-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="20947-206">默认情况下，内容控件是空的以便可以添加自己的内容。</span><span class="sxs-lookup"><span data-stu-id="20947-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="20947-207">如果您可能喜欢它们使用 ContentPlaceHolder 控件在母版页上的内容，只需单击智能标记符号 （在右上角的控件的小黑色箭头），然后选择*默认为母版内容*从智能标记，如中所示**图 8**。</span><span class="sxs-lookup"><span data-stu-id="20947-207">If youd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="20947-208">执行此操作时，菜单项将变为*创建自定义内容*。</span><span class="sxs-lookup"><span data-stu-id="20947-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="20947-209">此时，单击从母版页允许您定义该特定的内容控件的自定义内容中删除内容。</span><span class="sxs-lookup"><span data-stu-id="20947-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>


![设置默认为母版页的页面内容的内容控件](master-pages/_static/image4.gif)

<span data-ttu-id="20947-211">**图 7**： 将内容控件设置为默认为母版页的页面内容</span><span class="sxs-lookup"><span data-stu-id="20947-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>


## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="20947-212">连接母版页和内容页面</span><span class="sxs-lookup"><span data-stu-id="20947-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="20947-213">母版页和内容页之间的关联可以配置在四种不同方法之一：</span><span class="sxs-lookup"><span data-stu-id="20947-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="20947-214"><strong>MasterPageFile</strong>属性的@Page指令</span><span class="sxs-lookup"><span data-stu-id="20947-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="20947-215">设置**Page.MasterPageFile**在代码中的属性。</span><span class="sxs-lookup"><span data-stu-id="20947-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="20947-216">**&lt;页面&gt;** 应用程序配置文件 (web.config 应用程序的根文件夹中) 中的元素</span><span class="sxs-lookup"><span data-stu-id="20947-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="20947-217">**&lt;页面&gt;** 子文件夹配置文件 (web.config 的子文件夹中) 中的元素</span><span class="sxs-lookup"><span data-stu-id="20947-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="20947-218">MasterPageFile 特性</span><span class="sxs-lookup"><span data-stu-id="20947-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="20947-219">MasterPageFile 属性轻松应用于特定的 ASP.NET 页面的母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="20947-220">它也是用来检查时应用主页面的方法**选择母版页**复选框为您在练习 1 中所做。</span><span class="sxs-lookup"><span data-stu-id="20947-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="20947-221">在代码中设置 Page.MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="20947-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="20947-222">通过在代码中设置的 MasterPageFile 属性，可以将特定母版页应用到你在运行时的内容。</span><span class="sxs-lookup"><span data-stu-id="20947-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="20947-223">这是你可能需要应用基于用户角色或某些其他条件的特定主页面非常有用。</span><span class="sxs-lookup"><span data-stu-id="20947-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="20947-224">MasterPageFile 属性必须设置 PreInit 方法中。</span><span class="sxs-lookup"><span data-stu-id="20947-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="20947-225">如果将其设置 PreInit 方法后，将引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="20947-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="20947-226">在其设置此属性页还必须具有一个内容控件为顶级控件的页。</span><span class="sxs-lookup"><span data-stu-id="20947-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="20947-227">否则将引发 HttpException MasterPageFile 属性设置时。</span><span class="sxs-lookup"><span data-stu-id="20947-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="20947-228">使用&lt;页面&gt;元素</span><span class="sxs-lookup"><span data-stu-id="20947-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="20947-229">通过将 masterPageFile 属性设置配置页面母版页&lt;页面&gt;web.config 文件的元素。</span><span class="sxs-lookup"><span data-stu-id="20947-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="20947-230">使用此方法时，请注意应用程序结构中较低级别的 web.config 文件来覆盖此设置。</span><span class="sxs-lookup"><span data-stu-id="20947-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="20947-231">在中设置任何 MasterPageFile 属性@Page指令还会覆盖此设置。</span><span class="sxs-lookup"><span data-stu-id="20947-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="20947-232">使用&lt;pages&gt;元素，可以轻松地创建<em>master</em>可重写如有必要在特定文件夹或文件中的母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-232">Using the &lt;pages&gt; element makes it simple to create a <em>master</em> master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="20947-233">母版页中的属性</span><span class="sxs-lookup"><span data-stu-id="20947-233">Properties in Master Pages</span></span>

<span data-ttu-id="20947-234">母版页上可以只需使这些属性中的母版页的公共公开属性。</span><span class="sxs-lookup"><span data-stu-id="20947-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="20947-235">例如，下面的代码定义一个名为 SomeProperty 属性：</span><span class="sxs-lookup"><span data-stu-id="20947-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="20947-236">若要从内容页访问 SomeProperty 属性，您将需要使用主属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="20947-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="20947-237">嵌套母版页</span><span class="sxs-lookup"><span data-stu-id="20947-237">Nesting Master Pages</span></span>

<span data-ttu-id="20947-238">母版页是确保在大型 Web 应用程序的常见的外观和感觉的完美解决方案。</span><span class="sxs-lookup"><span data-stu-id="20947-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="20947-239">但是，不常见具有大型网站共享一个公共接口的某些部分，而其他部分共享使用不同的接口。</span><span class="sxs-lookup"><span data-stu-id="20947-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="20947-240">若要解决这种需求，多个主页面是一个完美的解决方案。</span><span class="sxs-lookup"><span data-stu-id="20947-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="20947-241">但是，仍然无法解决这一事实，大型应用程序可能具有在所有页面之间共享某些组件 （如菜单，例如） 和仅在站点的某些部分之间共享其他组件。</span><span class="sxs-lookup"><span data-stu-id="20947-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="20947-242">对于该类型的情况下，嵌套的母版页可以很好地满足需要。</span><span class="sxs-lookup"><span data-stu-id="20947-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="20947-243">如您所见，普通的主页面组成一个母版页和内容页。</span><span class="sxs-lookup"><span data-stu-id="20947-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="20947-244">在嵌套的母版页的情况下，有两个主页面; 例如：父 master 和子 master。</span><span class="sxs-lookup"><span data-stu-id="20947-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="20947-245">子主页面也是内容页面，并且其主父母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="20947-246">下面是典型的主页面的代码：</span><span class="sxs-lookup"><span data-stu-id="20947-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="20947-247">在嵌套母版页方案中，这将是父 master。</span><span class="sxs-lookup"><span data-stu-id="20947-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="20947-248">另一个主页面将作为其主页面，使用此页，该代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="20947-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="20947-249">请注意，在此方案中，子 master 还父级主页的内容页面。</span><span class="sxs-lookup"><span data-stu-id="20947-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="20947-250">所有子母版页的内容显示在内容控件，可从父 ContentPlaceHolder 控件获取其内容。</span><span class="sxs-lookup"><span data-stu-id="20947-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="20947-251">设计器支持不可用于嵌套的母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="20947-252">当你要开发使用嵌套的母版时，需要使用源视图。</span><span class="sxs-lookup"><span data-stu-id="20947-252">When you are developing using nested masters, you will need to use source view.</span></span>


<span data-ttu-id="20947-253">此视频演示了如何使用嵌套的母版页。</span><span class="sxs-lookup"><span data-stu-id="20947-253">This video shows a walkthrough of using nested master pages.</span></span>


![](master-pages/_static/image1.png)


[<span data-ttu-id="20947-254">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="20947-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)


![选择母版页](master-pages/_static/image4.jpg)

<span data-ttu-id="20947-256">**图 8**： 选择母版页</span><span class="sxs-lookup"><span data-stu-id="20947-256">**Figure 8**: Selecting a Master Page</span></span>
