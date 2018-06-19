---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |Microsoft 文档
author: microsoft
description: 成功的网站的关键组件之一是一致的外观和感觉。 在 ASP.NET 中 1.x，开发人员用于用户控件复制常见页 elem....
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: f45dd9704f665244d2a48ec000326f6e98984e4f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30885094"
---
<a name="master-pages"></a><span data-ttu-id="38007-104">母版页</span><span class="sxs-lookup"><span data-stu-id="38007-104">Master Pages</span></span>
====================
<span data-ttu-id="38007-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="38007-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="38007-106">成功的网站的关键组件之一是一致的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="38007-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="38007-107">在 ASP.NET 中 1.x，开发人员使用用户控件在 Web 应用程序上复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="38007-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="38007-108">虽然这的确是一个可行的解决方案，则使用用户控件也具有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="38007-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="38007-109">例如，用户控件的位置中的更改需要在站点之间对多个页的更改。</span><span class="sxs-lookup"><span data-stu-id="38007-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="38007-110">用户控件也不会呈现在之后插入页面上的设计视图中。</span><span class="sxs-lookup"><span data-stu-id="38007-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>


<span data-ttu-id="38007-111">成功的网站的关键组件之一是一致的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="38007-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="38007-112">在 ASP.NET 中 1.x，开发人员使用用户控件在 Web 应用程序上复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="38007-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="38007-113">虽然这的确是一个可行的解决方案，则使用用户控件也具有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="38007-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="38007-114">例如，用户控件的位置中的更改需要在站点之间对多个页的更改。</span><span class="sxs-lookup"><span data-stu-id="38007-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="38007-115">用户控件也不会呈现在之后插入页面上的设计视图中。</span><span class="sxs-lookup"><span data-stu-id="38007-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="38007-116">ASP.NET 2.0 引入了 Master 页作为一种维护一致的外观和感觉，而且如你很快就会看到，Master 页通过用户控件方法表示的重大进步。</span><span class="sxs-lookup"><span data-stu-id="38007-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="38007-117">为什么主页？</span><span class="sxs-lookup"><span data-stu-id="38007-117">Why Master Pages?</span></span>

<span data-ttu-id="38007-118">你可能想知道为什么主控页所需在 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="38007-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="38007-119">毕竟，网站开发人员已使用用户控件在 ASP.NET 中 1.x 共享页面之间的内容区域。</span><span class="sxs-lookup"><span data-stu-id="38007-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="38007-120">实际原因有多种原因用户控件是用于创建通用布局的不太比最佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="38007-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="38007-121">用户控件实际上未定义页面布局。</span><span class="sxs-lookup"><span data-stu-id="38007-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="38007-122">相反，它们定义的布局和页面的一个部分的功能。</span><span class="sxs-lookup"><span data-stu-id="38007-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="38007-123">这两者之间的差异非常重要，因为它使用户控制解决方案的可管理性困难得多。</span><span class="sxs-lookup"><span data-stu-id="38007-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="38007-124">例如，如果你想要更改你的页面上的用户控件的位置，你必须编辑用户控件在其显示的实际页。</span><span class="sxs-lookup"><span data-stu-id="38007-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="38007-125">如果你有仅几个页面，但在大型站点中，我们很快就会站点管理非常困难，这是微调 ！</span><span class="sxs-lookup"><span data-stu-id="38007-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="38007-126">用于定义常用布局使用用户控件的另一个缺点 ASP.NET 本身的体系结构中已取得 root 权限。</span><span class="sxs-lookup"><span data-stu-id="38007-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="38007-127">如果更改用户控件的任何公共成员，它将要求你重新编译所有使用该用户控件的页面。</span><span class="sxs-lookup"><span data-stu-id="38007-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="38007-128">反过来，ASP.NET 将然后重新 JIT 页面首次访问。</span><span class="sxs-lookup"><span data-stu-id="38007-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="38007-129">此操作，请再次生成不可扩展的体系结构和较大的站点的站点管理问题。</span><span class="sxs-lookup"><span data-stu-id="38007-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="38007-130">通过在 ASP.NET 2.0 的主控页，这两个这些问题 （以及更多） 可以很好地进行寻址。</span><span class="sxs-lookup"><span data-stu-id="38007-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="38007-131">如何母版页的工作原理</span><span class="sxs-lookup"><span data-stu-id="38007-131">How Master Pages Work</span></span>

<span data-ttu-id="38007-132">母版页是类似于其他页面的模板。</span><span class="sxs-lookup"><span data-stu-id="38007-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="38007-133">应在其他页 （即菜单、 边框、 等） 之间共享的页面元素添加到母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="38007-134">当新页面添加到该站点时，你可以将其与母版页中关联。</span><span class="sxs-lookup"><span data-stu-id="38007-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="38007-135">调用页与母版页的**内容页**。</span><span class="sxs-lookup"><span data-stu-id="38007-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="38007-136">默认情况下，内容页面采用从主控页的外观。</span><span class="sxs-lookup"><span data-stu-id="38007-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="38007-137">但是，当你创建母板页，你可以定义内容页可以将其自己的内容替换页面的部分。</span><span class="sxs-lookup"><span data-stu-id="38007-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="38007-138">这些部分定义使用在 ASP.NET 2.0; 中引入一个新的控件**ContentPlaceHolder**控件。</span><span class="sxs-lookup"><span data-stu-id="38007-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="38007-139">母版页可以包含任意数量的 ContentPlaceHolder 控件 （或全部都不。）在内容页上会出现的内部的 ContentPlaceHolder 控件中的内容**内容**控件，在 ASP.NET 2.0 中的另一个新控件。</span><span class="sxs-lookup"><span data-stu-id="38007-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="38007-140">默认情况下，内容控件的内容页为空，以便你可以提供自己的内容。</span><span class="sxs-lookup"><span data-stu-id="38007-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="38007-141">如果你想要使用内容控件内母版页中的内容，则可以执行因此，当你将看到更高版本在此模块。</span><span class="sxs-lookup"><span data-stu-id="38007-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="38007-142">内容控件映射到内容控件的 ContentPlaceHolderID 属性通过 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="38007-143">地图下面的代码到母版页上名为 mainBody ContentPlaceHolder 控件的内容控件。</span><span class="sxs-lookup"><span data-stu-id="38007-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="38007-144">通常，你将能听到描述的其他页面的基类为母版页的人员。</span><span class="sxs-lookup"><span data-stu-id="38007-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="38007-145">这是实际事实并非如此。</span><span class="sxs-lookup"><span data-stu-id="38007-145">Thats actually not true.</span></span> <span data-ttu-id="38007-146">母版页和内容页之间的关系不是继承。</span><span class="sxs-lookup"><span data-stu-id="38007-146">The relationship between master pages and content pages is not one of inheritance.</span></span>


<span data-ttu-id="38007-147">**图 1**显示母版页和关联的内容页，在 Visual Studio 2005 中显示。</span><span class="sxs-lookup"><span data-stu-id="38007-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="38007-148">你可以看到在母版页和相应的 ContentPlaceHolder 控件内容在内容页中的控件。</span><span class="sxs-lookup"><span data-stu-id="38007-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="38007-149">请注意，在 ContentPlaceHolder 之外的母版页内容可见但在内容页中灰显。</span><span class="sxs-lookup"><span data-stu-id="38007-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="38007-150">可以通过内容页取代仅 ContentPlaceHolder 内的内容。</span><span class="sxs-lookup"><span data-stu-id="38007-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="38007-151">所有其他来自母版页的内容不可变。</span><span class="sxs-lookup"><span data-stu-id="38007-151">All other content that comes from the master page is immutable.</span></span>


![主控页和其关联的内容页](master-pages/_static/image1.jpg)

<span data-ttu-id="38007-153">**图 1**： 主控页和其关联的内容页</span><span class="sxs-lookup"><span data-stu-id="38007-153">**Figure 1**: A master page and its associated content page</span></span>


## <a name="creating-a-master-page"></a><span data-ttu-id="38007-154">创建 Master 页</span><span class="sxs-lookup"><span data-stu-id="38007-154">Creating a Master Page</span></span>

<span data-ttu-id="38007-155">若要创建新的母版页：</span><span class="sxs-lookup"><span data-stu-id="38007-155">To create a new master page:</span></span>

1. <span data-ttu-id="38007-156">打开 Visual Studio 2005 并创建新网站。</span><span class="sxs-lookup"><span data-stu-id="38007-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="38007-157">单击新建文件，文件。</span><span class="sxs-lookup"><span data-stu-id="38007-157">Click File, New, File.</span></span>
3. <span data-ttu-id="38007-158">从添加新项对话框中选择主文件中所示**图 2**。</span><span class="sxs-lookup"><span data-stu-id="38007-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="38007-159">单击添加。</span><span class="sxs-lookup"><span data-stu-id="38007-159">Click Add.</span></span>


![创建一个新的主页面](master-pages/_static/image2.jpg)

<span data-ttu-id="38007-161">**图 2**： 创建一个新的主页面</span><span class="sxs-lookup"><span data-stu-id="38007-161">**Figure 2**: Creating a New Master Page</span></span>


<span data-ttu-id="38007-162">请注意，母版页的文件扩展名是<em>.master</em>。</span><span class="sxs-lookup"><span data-stu-id="38007-162">Notice that the file extension for a master page is <em>.master</em>.</span></span> <span data-ttu-id="38007-163">这是一个母版页上与普通页不同的方式。</span><span class="sxs-lookup"><span data-stu-id="38007-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="38007-164">其他主要差别在于，替代@Page指令，母版页包含@Master指令。</span><span class="sxs-lookup"><span data-stu-id="38007-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="38007-165">切换到源视图的主页面你刚刚创建，并检查代码。</span><span class="sxs-lookup"><span data-stu-id="38007-165">Switch to Source View for the master page youve just created and review the code.</span></span>

<span data-ttu-id="38007-166">默认情况下，新的母版页将具有一个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="38007-167">在大多数情况下，它更有意义要先创建常见的页面元素，然后插入 ContentPlaceHolder 控件需要自定义内容。</span><span class="sxs-lookup"><span data-stu-id="38007-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="38007-168">在这些情况下，开发人员将想要删除默认 ContentPlaceHolder 控件并将插入新记录，由于页开发。</span><span class="sxs-lookup"><span data-stu-id="38007-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="38007-169">ContentPlaceHolder 控件不调整它们显示调整大小控点的情况下。</span><span class="sxs-lookup"><span data-stu-id="38007-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="38007-170">ContentPlaceHolder 控件大小自动基于有一个例外; 它包含的内容如果块元素内的 ContentPlaceHolder 控件置于如表单元格上时，它将根据元素的大小的大小。</span><span class="sxs-lookup"><span data-stu-id="38007-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="38007-171">实验室 1 使用母版页</span><span class="sxs-lookup"><span data-stu-id="38007-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="38007-172">在本实验中，将创建新的主页面，并定义三个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="38007-173">然后，你将创建一个新的内容页，并将中至少一个 ContentPlaceHolder 控件的内容。</span><span class="sxs-lookup"><span data-stu-id="38007-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="38007-174">创建母版页和插入 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="38007-175">创建新的母版页上按上文所述。</span><span class="sxs-lookup"><span data-stu-id="38007-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="38007-176">删除默认 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="38007-177">通过单击控件的阴影上边框选择 ContentPlaceHolder 控件，然后删除它按你键盘上的 DEL 键。</span><span class="sxs-lookup"><span data-stu-id="38007-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="38007-178">插入新表使用*标头和端*模板图 3 中所示。</span><span class="sxs-lookup"><span data-stu-id="38007-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="38007-179">将宽度和高度更改为 90%，以使整个表设计器中可见。</span><span class="sxs-lookup"><span data-stu-id="38007-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>


![](master-pages/_static/image3.jpg)

<span data-ttu-id="38007-180">**图 3**</span><span class="sxs-lookup"><span data-stu-id="38007-180">**Figure 3**</span></span>


1. <span data-ttu-id="38007-181">将光标置于表的每个单元格并设置*垂直*属性*顶部*。</span><span class="sxs-lookup"><span data-stu-id="38007-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="38007-182">从工具箱中，将 ContentPlaceHolder 控件插入顶部的单元格的表 （标头单元。）</span><span class="sxs-lookup"><span data-stu-id="38007-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="38007-183">当插入此 ContentPlaceHolder 控件时，你将注意到行高将几乎整个页面占用，如图 4 中所示。</span><span class="sxs-lookup"><span data-stu-id="38007-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="38007-184">别担心，在此点。</span><span class="sxs-lookup"><span data-stu-id="38007-184">Dont be concerned about that at this point.</span></span>


![空的空间是在相同单元作为 ContentPlaceHolder](master-pages/_static/image1.gif)

<span data-ttu-id="38007-186">**图 4**： 空白区域是在相同单元作为 ContentPlaceHolder</span><span class="sxs-lookup"><span data-stu-id="38007-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>


1. <span data-ttu-id="38007-187">将 ContentPlaceHolder 控件放在其他两个单元格。</span><span class="sxs-lookup"><span data-stu-id="38007-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="38007-188">后已插入其他 ContentPlaceHolder 控件，如你所料，应为表格单元格的大小。</span><span class="sxs-lookup"><span data-stu-id="38007-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="38007-189">页面现在应如下所示中显示的网页**图 5**。</span><span class="sxs-lookup"><span data-stu-id="38007-189">The page should now look like the page shown in **figure 5**.</span></span>


![与所有 ContentPlaceHolder 控件 Master。](master-pages/_static/image2.gif)

<span data-ttu-id="38007-192">**图 5**： 所有 ContentPlaceHolder 控件母版。</span><span class="sxs-lookup"><span data-stu-id="38007-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="38007-193">请注意标题单元格的单元格高度现它应该是什么</span><span class="sxs-lookup"><span data-stu-id="38007-193">Notice that the cell height for the header cell is now what it should be</span></span>


1. <span data-ttu-id="38007-194">输入所选的一些文本到每个三个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="38007-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="38007-195">Exercise1.master 另存母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="38007-196">创建新的 Web 窗体并将其与 exercise1.master 母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="38007-197">选择文件，新、 文件在 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="38007-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="38007-198">选择**Web 窗体**在添加新项对话框。</span><span class="sxs-lookup"><span data-stu-id="38007-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="38007-199">请确保选中选择母版页复选框，如图 6 中所示。</span><span class="sxs-lookup"><span data-stu-id="38007-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>


![添加一个新的内容页](master-pages/_static/image3.gif)

<span data-ttu-id="38007-201">**图 6**： 添加一个新的内容页</span><span class="sxs-lookup"><span data-stu-id="38007-201">**Figure 6**: Adding a new Content Page</span></span>


1. <span data-ttu-id="38007-202">单击添加。</span><span class="sxs-lookup"><span data-stu-id="38007-202">Click Add.</span></span>
2. <span data-ttu-id="38007-203">选择 exercise1.master 在选择母版页对话框图 7 中所示。</span><span class="sxs-lookup"><span data-stu-id="38007-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="38007-204">单击确定以添加新的内容页。</span><span class="sxs-lookup"><span data-stu-id="38007-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="38007-205">新内容页将显示在 Visual Studio 在主页上每个 ContentPlaceHolder 控件的一个内容控件。</span><span class="sxs-lookup"><span data-stu-id="38007-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="38007-206">默认情况下，内容控件是空的以便您可以添加自己的内容。</span><span class="sxs-lookup"><span data-stu-id="38007-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="38007-207">如果想再使用母版页上的 ContentPlaceHolder 控件中的内容，只需单击智能标记符号 （控件的右上角的小黑色箭头），并选择*默认为母版内容*从所示的智能标记**图 8**。</span><span class="sxs-lookup"><span data-stu-id="38007-207">If youd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="38007-208">执行此操作时，菜单项更改为*创建自定义内容*。</span><span class="sxs-lookup"><span data-stu-id="38007-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="38007-209">此时，单击删除母版页让你能够定义为该特定的内容控件的自定义内容的内容。</span><span class="sxs-lookup"><span data-stu-id="38007-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>


![设置默认为母版页页内容的内容控件](master-pages/_static/image4.gif)

<span data-ttu-id="38007-211">**图 7**： 将内容控件设置为默认为母版页页内容</span><span class="sxs-lookup"><span data-stu-id="38007-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>


## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="38007-212">连接母版页和内容页</span><span class="sxs-lookup"><span data-stu-id="38007-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="38007-213">可以四种不同方式之一中配置母版页和内容页之间的关联：</span><span class="sxs-lookup"><span data-stu-id="38007-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="38007-214"><strong>MasterPageFile</strong>属性@Page指令</span><span class="sxs-lookup"><span data-stu-id="38007-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="38007-215">设置**Page.MasterPageFile**在代码中的属性。</span><span class="sxs-lookup"><span data-stu-id="38007-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="38007-216">**&lt;页&gt;** 应用程序配置文件 (web.config 应用程序的根文件夹中) 中的元素</span><span class="sxs-lookup"><span data-stu-id="38007-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="38007-217">**&lt;页&gt;** 子文件夹配置文件 (web.config 的子文件夹中) 中的元素</span><span class="sxs-lookup"><span data-stu-id="38007-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="38007-218">MasterPageFile 属性</span><span class="sxs-lookup"><span data-stu-id="38007-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="38007-219">MasterPageFile 属性，可以轻松将母版页应用于特定的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="38007-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="38007-220">它也是用于检查时应用主控页的方法**选择母版页**复选框为你未在练习 1 中。</span><span class="sxs-lookup"><span data-stu-id="38007-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="38007-221">在代码中设置 Page.MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="38007-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="38007-222">通过在代码中设置 MasterPageFile 属性，你可以在运行时你的内容应用特定的母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="38007-223">这可在情况下，你可能需要将特定母版页基于用户角色或某些其他条件应用。</span><span class="sxs-lookup"><span data-stu-id="38007-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="38007-224">MasterPageFile 属性必须设置 PreInit 方法中。</span><span class="sxs-lookup"><span data-stu-id="38007-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="38007-225">如果设置 PreInit 方法后，将引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="38007-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="38007-226">在其设置此属性页还必须具有内容的控件为顶级控件页。</span><span class="sxs-lookup"><span data-stu-id="38007-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="38007-227">否则 MasterPageFile 属性设置时，将引发 HttpException。</span><span class="sxs-lookup"><span data-stu-id="38007-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="38007-228">使用&lt;页&gt;元素</span><span class="sxs-lookup"><span data-stu-id="38007-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="38007-229">你可以通过将 masterPageFile 属性设置配置页母版页&lt;页&gt;web.config 文件的元素。</span><span class="sxs-lookup"><span data-stu-id="38007-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="38007-230">使用此方法时，记住应用程序结构中较低级别的 web.config 文件可以重写此设置。</span><span class="sxs-lookup"><span data-stu-id="38007-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="38007-231">在中设置任何 MasterPageFile 属性@Page指令还将重写此设置。</span><span class="sxs-lookup"><span data-stu-id="38007-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="38007-232">使用&lt;页&gt;元素可以很容易地创建<em>master</em>母版页可以重写如有必要在特定文件夹或文件中。</span><span class="sxs-lookup"><span data-stu-id="38007-232">Using the &lt;pages&gt; element makes it simple to create a <em>master</em> master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="38007-233">母版页中的属性</span><span class="sxs-lookup"><span data-stu-id="38007-233">Properties in Master Pages</span></span>

<span data-ttu-id="38007-234">母版页可以公开只需使这些属性母版页中的公共属性。</span><span class="sxs-lookup"><span data-stu-id="38007-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="38007-235">例如，下面的代码定义一个名为 SomeProperty 属性：</span><span class="sxs-lookup"><span data-stu-id="38007-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="38007-236">若要从内容页访问 SomeProperty 属性，你将需要使用主属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="38007-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="38007-237">嵌套母版页</span><span class="sxs-lookup"><span data-stu-id="38007-237">Nesting Master Pages</span></span>

<span data-ttu-id="38007-238">母版页是完美的解决方案，确保跨大型 Web 应用程序的常见的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="38007-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="38007-239">但是，不少见具有大型站点共享一个公共接口的某些部分，而其他部分共享一个不同的接口。</span><span class="sxs-lookup"><span data-stu-id="38007-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="38007-240">若要解决这种需求，多个母版页是完美的解决方案。</span><span class="sxs-lookup"><span data-stu-id="38007-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="38007-241">但是，这样仍然不解决大型应用程序可能具有在所有页之间共享某些组件 （如菜单，例如） 和其他仅在站点的某些部分之间共享的组件。</span><span class="sxs-lookup"><span data-stu-id="38007-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="38007-242">对于该类型的情况下，嵌套的母版页精美填充需要。</span><span class="sxs-lookup"><span data-stu-id="38007-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="38007-243">如你所见，正常母版页由母版页和内容页组成。</span><span class="sxs-lookup"><span data-stu-id="38007-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="38007-244">在嵌套的母版页的情况下，有两个主页面; 例如：父主服务器并子 master。</span><span class="sxs-lookup"><span data-stu-id="38007-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="38007-245">子母版页也是内容页并且其主父母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="38007-246">下面是典型的主控页的代码：</span><span class="sxs-lookup"><span data-stu-id="38007-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="38007-247">在嵌套的主方案中，这将是父 master。</span><span class="sxs-lookup"><span data-stu-id="38007-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="38007-248">另一个母版页将使用此页为其主页面，并且该代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="38007-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="38007-249">请注意，在此方案中，子主也是父级主页的内容页。</span><span class="sxs-lookup"><span data-stu-id="38007-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="38007-250">所有子母版页的内容显示在从父 ContentPlaceHolder 控件获取其内容的内容控件内。</span><span class="sxs-lookup"><span data-stu-id="38007-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="38007-251">设计器支持不可用于嵌套的母版页。</span><span class="sxs-lookup"><span data-stu-id="38007-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="38007-252">当你正在开发使用嵌套母版时，你将需要使用源视图。</span><span class="sxs-lookup"><span data-stu-id="38007-252">When you are developing using nested masters, you will need to use source view.</span></span>


<span data-ttu-id="38007-253">本视频介绍了使用嵌套的母版页的演练。</span><span class="sxs-lookup"><span data-stu-id="38007-253">This video shows a walkthrough of using nested master pages.</span></span>


![](master-pages/_static/image1.png)


[<span data-ttu-id="38007-254">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="38007-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)


![选择 Master 页](master-pages/_static/image4.jpg)

<span data-ttu-id="38007-256">**图 8**： 选择母版页</span><span class="sxs-lookup"><span data-stu-id="38007-256">**Figure 8**: Selecting a Master Page</span></span>
