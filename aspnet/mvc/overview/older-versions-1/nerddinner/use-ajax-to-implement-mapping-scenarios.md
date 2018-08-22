---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 实现映射方案 |Microsoft Docs
author: microsoft
description: 步骤 11 显示了如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得创建、 编辑或查看 dinners，若要查看 l 的用户...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f7de23ca46e6dc00fe8075e28068a8b3f95d02cd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823545"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="b89d4-103">使用 AJAX 实现映射方案</span><span class="sxs-lookup"><span data-stu-id="b89d4-103">Use AJAX to Implement Mapping Scenarios</span></span>
====================
<span data-ttu-id="b89d4-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b89d4-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b89d4-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b89d4-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b89d4-106">这是一种免费的步骤 11 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b89d4-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b89d4-107">步骤 11 显示了如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得创建、 编辑或查看 dinners，若要以图形方式查看 dinner 的位置的用户。</span><span class="sxs-lookup"><span data-stu-id="b89d4-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="b89d4-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="b89d4-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="b89d4-109">NerdDinner 步骤 11： 将集成的 AJAX 映射</span><span class="sxs-lookup"><span data-stu-id="b89d4-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="b89d4-110">我们现在将使我们的应用程序一些更直观地令人兴奋的通过集成的 AJAX 映射支持。</span><span class="sxs-lookup"><span data-stu-id="b89d4-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="b89d4-111">这将使创建、 编辑或查看 dinners，若要以图形方式查看 dinner 的位置的用户。</span><span class="sxs-lookup"><span data-stu-id="b89d4-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="b89d4-112">创建映射分部视图</span><span class="sxs-lookup"><span data-stu-id="b89d4-112">Creating a Map Partial View</span></span>

<span data-ttu-id="b89d4-113">我们将在我们的应用程序的多个位置中使用映射功能。</span><span class="sxs-lookup"><span data-stu-id="b89d4-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="b89d4-114">保留我们的代码 DRY 我们将封装在单一的部分模板，我们可以重新使用跨多个控制器操作和视图中的常见映射功能。</span><span class="sxs-lookup"><span data-stu-id="b89d4-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="b89d4-115">我们将此分部视图"map.ascx"命名和创建 \Views\Dinners 目录中。</span><span class="sxs-lookup"><span data-stu-id="b89d4-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="b89d4-116">我们可以创建 map.ascx 部分 \Views\Dinners 目录上右键单击并选择添加-&gt;查看菜单命令。</span><span class="sxs-lookup"><span data-stu-id="b89d4-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="b89d4-117">我们将视图命名为"Map.ascx"，检查为分部视图，并指示我们要将其传递强类型化"Dinner"model 类：</span><span class="sxs-lookup"><span data-stu-id="b89d4-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="b89d4-118">当我们单击"添加"按钮时将创建我们部分的模板。</span><span class="sxs-lookup"><span data-stu-id="b89d4-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="b89d4-119">然后，我们将更新 Map.ascx 文件具有以下内容：</span><span class="sxs-lookup"><span data-stu-id="b89d4-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="b89d4-120">第一个&lt;脚本&gt;引用指向 Microsoft 虚拟地球 6.2 映射库。</span><span class="sxs-lookup"><span data-stu-id="b89d4-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="b89d4-121">第二个&lt;脚本&gt;引用到 map.js 我们稍后将创建该文件将封装我们常见的 Javascript 映射逻辑点。</span><span class="sxs-lookup"><span data-stu-id="b89d4-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="b89d4-122">&lt;D i v id ="theMap"&gt;元素是 Virtual Earth 将用于承载该映射的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="b89d4-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="b89d4-123">然后，我们嵌入&lt;脚本&gt;包含特定于此视图的两个 JavaScript 函数的块。</span><span class="sxs-lookup"><span data-stu-id="b89d4-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="b89d4-124">第一个函数使用 jQuery 来布置页面准备好运行客户端脚本时执行的函数。</span><span class="sxs-lookup"><span data-stu-id="b89d4-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="b89d4-125">调用 LoadMap() 帮助器函数，我们将在我们 Map.js 的脚本文件加载 virtual earth 地图控件内定义。</span><span class="sxs-lookup"><span data-stu-id="b89d4-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="b89d4-126">第二个函数是将 pin 添加到标识的位置映射一个回调事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="b89d4-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="b89d4-127">请注意我们如何使用服务器端&lt;%= %&gt;要嵌入的纬度和经度的 Dinner 我们想要将映射到 JavaScript 的客户端脚本块内的块。</span><span class="sxs-lookup"><span data-stu-id="b89d4-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="b89d4-128">这是输出可由客户端脚本 （而无需单独 AJAX 调用回发到服务器中检索值 – 这可以更快） 的动态值的有用技术。</span><span class="sxs-lookup"><span data-stu-id="b89d4-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="b89d4-129">&lt;%= %&gt;块将执行服务器 – 上呈现视图时，并因此的 html 输出只是最终将有嵌入的 JavaScript 值 (例如： var 纬度 = 47.64312;)。</span><span class="sxs-lookup"><span data-stu-id="b89d4-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="b89d4-130">创建 Map.js 的实用程序库</span><span class="sxs-lookup"><span data-stu-id="b89d4-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="b89d4-131">让我们现在创建 Map.js 文件，我们可以用来封装我们的地图的 JavaScript 功能 （并实现更高版本的 LoadMap 和 LoadPin 方法）。</span><span class="sxs-lookup"><span data-stu-id="b89d4-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="b89d4-132">我们可以执行此操作上的 \Scripts 目录中我们的项目，右键单击，然后选择"添加-&gt;新项"菜单命令，选择 JScript 项目，并将其命名为"Map.js"。</span><span class="sxs-lookup"><span data-stu-id="b89d4-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="b89d4-133">下面是我们将添加的 JavaScript 代码将与 Virtual Earth 可以显示我们的地图和为我们 dinners 向其添加位置 pin 进行交互的 Map.js 文件：</span><span class="sxs-lookup"><span data-stu-id="b89d4-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="b89d4-134">与创建和编辑窗体集成映射</span><span class="sxs-lookup"><span data-stu-id="b89d4-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="b89d4-135">我们现在将与我们现有的创建和编辑方案集成映射支持。</span><span class="sxs-lookup"><span data-stu-id="b89d4-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="b89d4-136">好消息是这是非常简单的待办事项，并且不需要我们要更改任何控制器代码。</span><span class="sxs-lookup"><span data-stu-id="b89d4-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="b89d4-137">由于我们创建和编辑的视图共享常见"DinnerForm"分部视图来实现 dinner 窗体用户界面，我们可以在一个位置添加映射，并让使用它的这两种我们创建和编辑方案。</span><span class="sxs-lookup"><span data-stu-id="b89d4-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="b89d4-138">我们只需待办事项是打开 \Views\Dinners\DinnerForm.ascx 分部视图，并将其更新为包括新地图部分。</span><span class="sxs-lookup"><span data-stu-id="b89d4-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="b89d4-139">下面是添加映射后更新的 DinnerForm 外观 (注意： 为简洁起见以下代码段中省略了 HTML 窗体元素):</span><span class="sxs-lookup"><span data-stu-id="b89d4-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="b89d4-140">上面部分 DinnerForm 采用"DinnerFormViewModel"类型的对象作为其模型类型，（因为它需要一个 Dinner 对象，以及 SelectList 来填充 dropdownlist 的国家/地区）。</span><span class="sxs-lookup"><span data-stu-id="b89d4-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="b89d4-141">我们的地图部分只是需要类型"Dinner"的对象作为其模型的类型，并因此时呈现地图部分我们将仅的 Dinner 子属性 DinnerFormViewModel 向其传递：</span><span class="sxs-lookup"><span data-stu-id="b89d4-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="b89d4-142">我们添加到要附加到"地址"HTML 文本框的"模糊"事件部分使用 jQuery 的 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="b89d4-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="b89d4-143">您可能听说过"焦点"激发事件，当用户单击或选项卡在文本框。</span><span class="sxs-lookup"><span data-stu-id="b89d4-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="b89d4-144">相反是激发用户退出文本框时的"模糊"事件。</span><span class="sxs-lookup"><span data-stu-id="b89d4-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="b89d4-145">当发生此情况，而绘制地图上的新地址位置时，上述事件处理程序清除纬度和经度文本框值。</span><span class="sxs-lookup"><span data-stu-id="b89d4-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="b89d4-146">然后，我们 map.js 文件内定义一个回调事件处理程序将更新我们使用基于我们赋给它的地址的虚拟地球返回值的窗体上的经度和纬度的 textbox。</span><span class="sxs-lookup"><span data-stu-id="b89d4-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="b89d4-147">和现在我们我们再次运行应用程序并单击"主机 Dinner"选项卡将介绍的默认值将映射与我们的标准 Dinner 窗体元素一起显示：</span><span class="sxs-lookup"><span data-stu-id="b89d4-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="b89d4-148">后，我们键入一个地址，然后按 tab 离开，映射将动态更新以显示该位置，然后我们的事件处理程序将填充的位置值的纬度/经度文本框：</span><span class="sxs-lookup"><span data-stu-id="b89d4-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="b89d4-149">如果保存新 dinner，然后重新打开以进行编辑，我们会发现在页面加载时显示的映射位置：</span><span class="sxs-lookup"><span data-stu-id="b89d4-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="b89d4-150">每次更改地址字段时，将更新映射和纬度/经度坐标。</span><span class="sxs-lookup"><span data-stu-id="b89d4-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="b89d4-151">现在，该地图显示 Dinner 位置，我们还可以从正在可见文本框以改为隐藏的元素 （因为映射自动更新其每次输入一个地址时） 更改的纬度和经度的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="b89d4-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="b89d4-152">待办事项此我们将切换从使用 Html.TextBox() HTML 帮助器使用 Html.Hidden() 帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="b89d4-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="b89d4-153">和现在我们窗体更具用户友好性并避免显示原始纬度/经度 （此时，仍将它们存储在数据库中每个 Dinner 使用）：</span><span class="sxs-lookup"><span data-stu-id="b89d4-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="b89d4-154">将地图集成的详细信息视图</span><span class="sxs-lookup"><span data-stu-id="b89d4-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="b89d4-155">现在，我们已让我们与我们创建和编辑的方案，集成还将其与我们的详细信息方案集成的映射。</span><span class="sxs-lookup"><span data-stu-id="b89d4-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="b89d4-156">我们需要待办事项，只需调用&lt;%html.renderpartial("map"); %&gt;的详细信息视图中。</span><span class="sxs-lookup"><span data-stu-id="b89d4-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="b89d4-157">下面是完整的详细信息视图 （具有映射的集成） 的源代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="b89d4-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="b89d4-158">现在当用户导航到 /Dinners/详细信息 / [id] URL 他们将看到有关 dinner dinner 在地图上的位置的详细信息 （完成，但一个图钉，当悬停在显示的 dinner 标题和它的地址），并且具有指向 RSVP fo 的 AJAX 链接r 它：</span><span class="sxs-lookup"><span data-stu-id="b89d4-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="b89d4-159">在我们的数据库和存储库中实现位置搜索</span><span class="sxs-lookup"><span data-stu-id="b89d4-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="b89d4-160">为了完成我们的 AJAX 实现，让我们将映射添加到允许用户以图形方式搜索 dinners 接近的人们的应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="b89d4-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="b89d4-161">我们将首先实现我们有效地执行 Dinners 的基于位置的 radius 搜索的数据库和数据的存储库层中的支持。</span><span class="sxs-lookup"><span data-stu-id="b89d4-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="b89d4-162">我们可以使用新[地理空间功能的 SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)来实现此操作，或者我们可以使用 Gary Dryden 讨论文章中的 SQL 函数方法或： [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)和 Rob conery 专攻有关使用 LINQ to SQL 使用此处发表： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="b89d4-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="b89d4-163">若要实现这种技术，我们将打开"服务器资源管理器"在 Visual Studio 中，选择 NerdDinner 的数据库，然后右键单击"函数"下的子节点并选择要创建一个新"标量值函数":</span><span class="sxs-lookup"><span data-stu-id="b89d4-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="b89d4-164">然后粘贴以下 DistanceBetween 函数中：</span><span class="sxs-lookup"><span data-stu-id="b89d4-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="b89d4-165">然后，我们将在 SQL Server 中，我们将调用"NearestDinners"创建新的表值函数：</span><span class="sxs-lookup"><span data-stu-id="b89d4-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="b89d4-166">此"NearestDinners"表函数使用 DistanceBetween 帮助器函数来返回所有 Dinners 内 100 英里的纬度和经度我们提供它：</span><span class="sxs-lookup"><span data-stu-id="b89d4-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="b89d4-167">若要调用此函数，我们将首先打开 LINQ to SQL 设计器通过双击我们 \Models 目录内 NerdDinner.dbml 文件：</span><span class="sxs-lookup"><span data-stu-id="b89d4-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="b89d4-168">然后，我们会将 NearestDinners 和 DistanceBetween 函数拖到 LINQ 到 SQL 设计器中，这将导致它们要作为我们 LINQ 的方法添加到 SQL NerdDinnerDataContext 类：</span><span class="sxs-lookup"><span data-stu-id="b89d4-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="b89d4-169">我们可以在我们使用 NearestDinner 函数以返回即将推出的 DinnerRepository 类公开"FindByLocation"查询方法内的指定位置的 100 英里的 Dinners:</span><span class="sxs-lookup"><span data-stu-id="b89d4-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="b89d4-170">实现基于 JSON 的 AJAX 搜索操作方法</span><span class="sxs-lookup"><span data-stu-id="b89d4-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="b89d4-171">我们现在将实现控制器操作方法都使用了新的 FindByLocation() 存储库方法以返回可用于填充地图的 Dinner 数据的列表。</span><span class="sxs-lookup"><span data-stu-id="b89d4-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="b89d4-172">我们将使此操作方法返回返回 Dinner 数据采用 JSON （JavaScript 对象表示法） 格式，以便它可以轻松地操作客户端上使用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="b89d4-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="b89d4-173">若要实现这一点，我们将创建一个新"SearchController"类 \Controllers 目录上右键单击并选择添加-&gt;控制器菜单命令。</span><span class="sxs-lookup"><span data-stu-id="b89d4-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="b89d4-174">然后，我们将实现内新 SearchController 类，如下面的"SearchByLocation"操作方法：</span><span class="sxs-lookup"><span data-stu-id="b89d4-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="b89d4-175">SearchController SearchByLocation 操作方法在内部调用 DinnerRespository 获取一系列附近 dinners FindByLocation 方法。</span><span class="sxs-lookup"><span data-stu-id="b89d4-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRespository to get a list of nearby dinners.</span></span> <span data-ttu-id="b89d4-176">而不是 Dinner 对象直接返回到客户端，不过，它改为返回 JsonDinner 对象。</span><span class="sxs-lookup"><span data-stu-id="b89d4-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="b89d4-177">JsonDinner 类公开了一部分 Dinner 属性 (例如： 出于安全原因，它并不公开为 dinner 已接受的人员的名称)。</span><span class="sxs-lookup"><span data-stu-id="b89d4-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="b89d4-178">它还包括一个 RSVPCount 属性不存在上 Dinner – 和其动态计算通过关联与特定 dinner 的 RSVP 对象的计数。</span><span class="sxs-lookup"><span data-stu-id="b89d4-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="b89d4-179">我们然后控制器基类上使用 json （） 帮助器方法返回 dinners 使用基于 JSON 的传输格式的序列。</span><span class="sxs-lookup"><span data-stu-id="b89d4-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="b89d4-180">JSON 是用于表示简单的数据结构以标准文本格式。</span><span class="sxs-lookup"><span data-stu-id="b89d4-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="b89d4-181">下面是 JSON 格式的两个 JsonDinner 对象列表如下所示从我们的操作方法返回时的示例：</span><span class="sxs-lookup"><span data-stu-id="b89d4-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="b89d4-182">调用使用 jQuery 的基于 JSON 的 AJAX 方法</span><span class="sxs-lookup"><span data-stu-id="b89d4-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="b89d4-183">我们现已准备好更新主页上的 NerdDinner 应用程序使用 SearchController SearchByLocation 操作方法。</span><span class="sxs-lookup"><span data-stu-id="b89d4-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="b89d4-184">待办事项，我们将打开 /Views/Home/Index.aspx 视图模板并将其更新为具有一个 textbox，搜索按钮，我们的地图，和一个&lt;div&gt;名为 dinnerList 元素：</span><span class="sxs-lookup"><span data-stu-id="b89d4-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="b89d4-185">然后，我们可以将两个 JavaScript 函数添加到页面：</span><span class="sxs-lookup"><span data-stu-id="b89d4-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="b89d4-186">首次加载页面时，第一个 JavaScript 函数将加载映射。</span><span class="sxs-lookup"><span data-stu-id="b89d4-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="b89d4-187">JavaScript 第二个 JavaScript 函数绑定单击搜索按钮上的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="b89d4-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="b89d4-188">当按钮按下它将调用我们将添加到我们的 Map.js 文件的 FindDinnersGivenLocation() JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="b89d4-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="b89d4-189">此 FindDinnersGivenLocation() 函数将调用映射。在要居中于输入的位置的虚拟地球控件 find （)。</span><span class="sxs-lookup"><span data-stu-id="b89d4-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="b89d4-190">当虚拟地球地图服务返回时，该映射。Find （） 方法调用我们作为最后一个参数传递它 callbackUpdateMapDinners 回调方法。</span><span class="sxs-lookup"><span data-stu-id="b89d4-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="b89d4-191">CallbackUpdateMapDinners() 方法是在其中完成实际工作。</span><span class="sxs-lookup"><span data-stu-id="b89d4-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="b89d4-192">它使用 jQuery 的 $.post() 帮助器方法来执行对我们 SearchController SearchByLocation() 操作方法-将其传递的纬度和经度的新居中后的地图的 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="b89d4-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="b89d4-193">它定义 $.post() 帮助器方法完成时，将调用一个内联函数，并且从操作方法将传递它使用名为"dinners"的变量 SearchByLocation() 返回 JSON 格式的 dinner 结果。</span><span class="sxs-lookup"><span data-stu-id="b89d4-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="b89d4-194">然后在各个每个返回 dinner foreach，并使用 dinner 的纬度和经度和其他属性在地图上添加一个新的 pin。</span><span class="sxs-lookup"><span data-stu-id="b89d4-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="b89d4-195">它还添加到 HTML 列表右侧的映射 dinners 的 dinner 条目。</span><span class="sxs-lookup"><span data-stu-id="b89d4-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="b89d4-196">它然后电线向上图钉和 HTML 列表在悬停事件，以便当用户悬停其上时显示有关 dinner 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="b89d4-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="b89d4-197">和现在我们运行该应用程序并访问主页上我们将看到一幅地图。</span><span class="sxs-lookup"><span data-stu-id="b89d4-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="b89d4-198">当我们进入的城市名称映射将显示办公电话附近即将推出的 dinners:</span><span class="sxs-lookup"><span data-stu-id="b89d4-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="b89d4-199">将鼠标悬停 dinner 将显示其详细信息。</span><span class="sxs-lookup"><span data-stu-id="b89d4-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="b89d4-200">单击 Dinner 标题在气泡或 HTML 列表中的右侧端上将导航我们到 dinner – 我们可以然后根据需要响应：</span><span class="sxs-lookup"><span data-stu-id="b89d4-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="b89d4-201">下一步</span><span class="sxs-lookup"><span data-stu-id="b89d4-201">Next Step</span></span>

<span data-ttu-id="b89d4-202">我们现在实现了所有我们 NerdDinner 应用程序的应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="b89d4-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="b89d4-203">让我们现在看如何可以启用自动单元测试它。</span><span class="sxs-lookup"><span data-stu-id="b89d4-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b89d4-204">[上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="b89d4-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
