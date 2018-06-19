---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX 用于实现映射方案 |Microsoft 文档
author: microsoft
description: 步骤 11 演示如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得用户创建、 编辑或查看晚餐若要查看 l...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 4b3f1e46886c4c1f054e43768b0a44695d71bf09
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872710"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="56457-103">AJAX 用于实现映射方案</span><span class="sxs-lookup"><span data-stu-id="56457-103">Use AJAX to Implement Mapping Scenarios</span></span>
====================
<span data-ttu-id="56457-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="56457-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="56457-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="56457-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="56457-106">这是个免费的步骤 11 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="56457-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="56457-107">步骤 11 演示如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得用户创建、 编辑或查看晚餐若要以图形方式查看 dinner 的位置。</span><span class="sxs-lookup"><span data-stu-id="56457-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="56457-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="56457-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="56457-109">NerdDinner 步骤 11： 集成 AJAX 映射</span><span class="sxs-lookup"><span data-stu-id="56457-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="56457-110">我们现在将使我们的应用程序少量更为直观振奋人心通过集成 AJAX 映射支持。</span><span class="sxs-lookup"><span data-stu-id="56457-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="56457-111">这将启用用户创建、 编辑或查看晚餐若要以图形方式查看 dinner 的位置。</span><span class="sxs-lookup"><span data-stu-id="56457-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="56457-112">创建映射分部视图</span><span class="sxs-lookup"><span data-stu-id="56457-112">Creating a Map Partial View</span></span>

<span data-ttu-id="56457-113">我们将使用我们的应用程序中的多个位置中映射功能。</span><span class="sxs-lookup"><span data-stu-id="56457-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="56457-114">使我们代码干我们将封装在单个部分模板，我们可以重新使用跨多个控制器操作和视图中的常见映射功能。</span><span class="sxs-lookup"><span data-stu-id="56457-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="56457-115">我们将此分部视图"map.ascx"，创建 \Views\Dinners 目录中。</span><span class="sxs-lookup"><span data-stu-id="56457-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="56457-116">我们可以创建 map.ascx 部分 \Views\Dinners 目录上右键单击并选择添加-&gt;查看菜单命令。</span><span class="sxs-lookup"><span data-stu-id="56457-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="56457-117">我们将视图命名为"Map.ascx"、 检查为分部视图，以及指示我们要将其传递一个强类型化"Dinner"模型类：</span><span class="sxs-lookup"><span data-stu-id="56457-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="56457-118">当单击"添加"按钮时，我们将创建我们部分的模板。</span><span class="sxs-lookup"><span data-stu-id="56457-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="56457-119">然后，我们将更新 Map.ascx 文件具有以下内容：</span><span class="sxs-lookup"><span data-stu-id="56457-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="56457-120">第一个&lt;脚本&gt;引用指向 Microsoft 虚拟地球 6.2 映射库。</span><span class="sxs-lookup"><span data-stu-id="56457-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="56457-121">第二个&lt;脚本&gt;引用到 map.js 我们很快将创建该文件将封装我们常见 Javascript 映射逻辑点。</span><span class="sxs-lookup"><span data-stu-id="56457-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="56457-122">&lt;Div id ="theMap"&gt;元素是 HTML 容器 Virtual Earth 将用于托管代码图。</span><span class="sxs-lookup"><span data-stu-id="56457-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="56457-123">接下来是一个嵌入&lt;脚本&gt;包含特定于此视图的两个 JavaScript 函数的块。</span><span class="sxs-lookup"><span data-stu-id="56457-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="56457-124">第一个函数使用 jQuery 网络型时页已准备好运行客户端脚本执行的函数。</span><span class="sxs-lookup"><span data-stu-id="56457-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="56457-125">调用 LoadMap() helper 函数，我们将在要加载虚拟地球地图控件我们 Map.js 脚本文件内定义。</span><span class="sxs-lookup"><span data-stu-id="56457-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="56457-126">第二个函数是回调事件处理程序将 pin 添加到的映射中标识的位置。</span><span class="sxs-lookup"><span data-stu-id="56457-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="56457-127">请注意，我们如何使用服务器端&lt;%= %&gt;在嵌入的纬度和经度 Dinner 我们想要将映射到 JavaScript 客户端脚本块的内部块。</span><span class="sxs-lookup"><span data-stu-id="56457-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="56457-128">这是一种用于输出可以 （而无需单独 AJAX 调用返回到服务器以检索值 – 使其更快地） 使用的客户端脚本的动态值的有用技术。</span><span class="sxs-lookup"><span data-stu-id="56457-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="56457-129">&lt;%= %&gt;视图呈现在服务器上时，将执行块并因此的 html 输出只最终将得到嵌入的 JavaScript 值 (例如： var 纬度 = 47.64312;)。</span><span class="sxs-lookup"><span data-stu-id="56457-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="56457-130">创建 Map.js 实用程序库</span><span class="sxs-lookup"><span data-stu-id="56457-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="56457-131">让我们现在创建 Map.js 文件，我们可以用来封装我们映射的 JavaScript 功能 （和实现 LoadMap 和 LoadPin 上述两种方法）。</span><span class="sxs-lookup"><span data-stu-id="56457-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="56457-132">我们可以执行此操作通过 \Scripts 目录在我们的项目中，右键单击，然后选择"添加-&gt;新项"菜单命令，选择 JScript 项目中，并将其命名为"Map.js"。</span><span class="sxs-lookup"><span data-stu-id="56457-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="56457-133">下面是我们将添加的 JavaScript 代码将与 Virtual Earth 以显示我们映射并为我们晚餐向其中添加位置 pin 进行交互的 Map.js 文件：</span><span class="sxs-lookup"><span data-stu-id="56457-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="56457-134">与创建和编辑窗体中集成映射</span><span class="sxs-lookup"><span data-stu-id="56457-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="56457-135">我们现在将与我们现有的创建和编辑方案集成的映射支持。</span><span class="sxs-lookup"><span data-stu-id="56457-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="56457-136">好消息是这是非常简单的待办事项，不要求我们要更改任何我们控制器代码。</span><span class="sxs-lookup"><span data-stu-id="56457-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="56457-137">由于我们创建和编辑视图共享了常见的"DinnerForm"分部视图实现 dinner 窗体用户界面，因此我们可以在一个位置中添加地图并让使用它的这两种我们创建和编辑方案。</span><span class="sxs-lookup"><span data-stu-id="56457-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="56457-138">我们只需待办事项是打开 \Views\Dinners\DinnerForm.ascx 分部视图并将其更新为包括部分我们新映射。</span><span class="sxs-lookup"><span data-stu-id="56457-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="56457-139">下面是添加地图后更新的 DinnerForm 外观 (注意： 以下代码段为简洁起见中省略了 HTML 窗体元素):</span><span class="sxs-lookup"><span data-stu-id="56457-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="56457-140">上面部分 DinnerForm 将类型"DinnerFormViewModel"的对象作为其模型类型，（因为它需要一个 Dinner 对象，以及此时若要填充的国家/地区 dropdownlist）。</span><span class="sxs-lookup"><span data-stu-id="56457-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="56457-141">我们映射部分只要求类型"Dinner"的对象作为其模型类型，并因此当我们呈现地图部分我们是仅将该 Dinner 子属性的 DinnerFormViewModel 向方法传递：</span><span class="sxs-lookup"><span data-stu-id="56457-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="56457-142">JavaScript 函数我们已添加到部分使用 jQuery 要附加到"Address"HTML 文本框中的"模糊"事件。</span><span class="sxs-lookup"><span data-stu-id="56457-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="56457-143">您之前可能听对象"焦点"当用户单击时触发的事件或选项卡到文本框。</span><span class="sxs-lookup"><span data-stu-id="56457-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="56457-144">相反是当用户退出文本框中，将引发一个"模糊"事件。</span><span class="sxs-lookup"><span data-stu-id="56457-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="56457-145">在这种情况下，然后绘制我们图上的新地址位置时，上述的事件处理程序清除纬度和经度文本框中值。</span><span class="sxs-lookup"><span data-stu-id="56457-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="56457-146">我们在 map.js 文件内定义一个回调事件处理程序然后将更新的经度和纬度的文本框，我们使用由虚拟地球基于我们赋予了它的地址返回的值的窗体上。</span><span class="sxs-lookup"><span data-stu-id="56457-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="56457-147">现在我们运行一次，我们的应用程序并单击"主机 Dinner"选项卡，我们将看到默认的映射与我们的标准 Dinner 窗体元素一起显示：</span><span class="sxs-lookup"><span data-stu-id="56457-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="56457-148">当我们在地址中，键入，然后跳转消失时，映射将会动态更新以显示位置，然后我们事件处理程序将填充的位置值纬度/经度文本框中：</span><span class="sxs-lookup"><span data-stu-id="56457-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="56457-149">如果我们保存新 dinner，然后重新打开以进行编辑，我们将找到加载页面时，显示地图位置：</span><span class="sxs-lookup"><span data-stu-id="56457-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="56457-150">每次更改地址字段后，将更新映射和纬度/经度坐标。</span><span class="sxs-lookup"><span data-stu-id="56457-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="56457-151">现在，代码图显示了 Dinner 位置，我们还可以从正在可见的文本框中 （因为该映射自动更新其每次输入一个地址） 更改为隐藏的元素更改纬度和经度窗体字段。</span><span class="sxs-lookup"><span data-stu-id="56457-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="56457-152">待办事项这我们将从使用使用 Html.Hidden() 帮助器方法的 Html.TextBox() HTML 帮助程序切换：</span><span class="sxs-lookup"><span data-stu-id="56457-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="56457-153">现在我们窗体将并变得更加用户友好避免显示原始纬度/经度 （此时，仍将它们存储在数据库中每个 Dinner 与）：</span><span class="sxs-lookup"><span data-stu-id="56457-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="56457-154">将与详细信息视图中集成映射</span><span class="sxs-lookup"><span data-stu-id="56457-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="56457-155">现在，我们已与我们创建和编辑方案集成的映射，让我们还将它与我们的详细信息的方案。</span><span class="sxs-lookup"><span data-stu-id="56457-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="56457-156">我们只需待办事项是调用&lt;%html.renderpartial("map"); %&gt;详细信息视图中。</span><span class="sxs-lookup"><span data-stu-id="56457-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="56457-157">下面是源代码到 （具有映射集成） 的完整详细信息视图如下所示：</span><span class="sxs-lookup"><span data-stu-id="56457-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="56457-158">现在当某个用户导航到 /Dinners/详细信息 / [id] URL 他们将看到有关 dinner dinner 图上的位置的详细信息和 （完成，但图钉图标，当悬停在显示的标题 dinner 和它的地址），并且使用到的回复 fo AJAX 链接r 它：</span><span class="sxs-lookup"><span data-stu-id="56457-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="56457-159">在我们的数据库和存储库中实现位置搜索</span><span class="sxs-lookup"><span data-stu-id="56457-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="56457-160">若要完成关闭我们 AJAX 实现，让我们将地图添加到主页上的应用程序允许用户以图形方式搜索晚餐接近它们。</span><span class="sxs-lookup"><span data-stu-id="56457-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="56457-161">首先，我们将实现中我们来高效地执行晚餐基于位置的 radius 搜索的数据库和数据的存储库层的支持。</span><span class="sxs-lookup"><span data-stu-id="56457-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="56457-162">我们无法使用新[地理空间功能的 SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)来实现此操作，或者我们可以使用一种 SQL 函数方法，在此处文章中讨论 Gary Dryden 或： [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)和 Rob Conery有关此处使用 LINQ to SQL 的信息的博客： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="56457-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="56457-163">若要实现此方法，我们将打开"服务器资源管理器"在 Visual Studio 中，选择 NerdDinner 数据库中，，然后右键单击其下的"函数"子节点，选择创建一个新"标量值函数":</span><span class="sxs-lookup"><span data-stu-id="56457-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="56457-164">我们将然后粘贴以下 DistanceBetween 函数：</span><span class="sxs-lookup"><span data-stu-id="56457-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="56457-165">然后，我们将在 SQL Server 中，我们将调用"NearestDinners"创建新的表值函数：</span><span class="sxs-lookup"><span data-stu-id="56457-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="56457-166">此"NearestDinners"表函数使用 DistanceBetween 帮助器函数返回所有晚餐中 100 英里的纬度和经度我们提供它：</span><span class="sxs-lookup"><span data-stu-id="56457-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="56457-167">若要调用此函数，我们将首先打开 LINQ to SQL 设计器通过双击我们 \Models 目录中的 NerdDinner.dbml 文件：</span><span class="sxs-lookup"><span data-stu-id="56457-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="56457-168">然后，我们将将的 NearestDinners 和 DistanceBetween 函数拖动到 LINQ 到 SQL 设计器中，这将导致它们将作为我们 linq 的方法添加到 SQL NerdDinnerDataContext 类：</span><span class="sxs-lookup"><span data-stu-id="56457-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="56457-169">我们可以在我们使用 NearestDinner 函数返回即将到来的 DinnerRepository 类上公开"FindByLocation"查询方法内的指定位置的 100 英里的晚餐：</span><span class="sxs-lookup"><span data-stu-id="56457-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="56457-170">实现基于 JSON 的 AJAX 搜索操作方法</span><span class="sxs-lookup"><span data-stu-id="56457-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="56457-171">我们现在将实施充分利用新 FindByLocation() 存储库的方法返回可以用于填充地图的 Dinner 数据的列表的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="56457-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="56457-172">我们将使此操作方法返回回 Dinner 数据以 JSON （JavaScript 对象表示法） 格式，以便它可以容易地操作在客户端使用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="56457-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="56457-173">若要实现这一点，我们将创建一个新"SearchController"类 \Controllers 目录上右键单击并选择添加-&gt;控制器菜单命令。</span><span class="sxs-lookup"><span data-stu-id="56457-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="56457-174">然后，我们将实施区内新 SearchController 类，如下面的"SearchByLocation"操作方法：</span><span class="sxs-lookup"><span data-stu-id="56457-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="56457-175">SearchController SearchByLocation 操作方法内部调用 DinnerRespository 若要获取的附近晚餐列表 FindByLocation 方法。</span><span class="sxs-lookup"><span data-stu-id="56457-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRespository to get a list of nearby dinners.</span></span> <span data-ttu-id="56457-176">而不是直接向客户端返回 Dinner 对象，不过，它而是返回 JsonDinner 对象。</span><span class="sxs-lookup"><span data-stu-id="56457-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="56457-177">JsonDinner 类公开 Dinner 属性的子集 (例如： 出于安全考虑，它不会公开为 dinner 答复具有活动的人员的名称)。</span><span class="sxs-lookup"><span data-stu-id="56457-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="56457-178">它还包括一个 RSVPCount 属性，不在 Dinner – 上存在且其动态计算通过计算与特定 dinner 关联的回复对象的数量。</span><span class="sxs-lookup"><span data-stu-id="56457-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="56457-179">我们然后将控制器基类上使用 Json() 帮助器方法来返回晚餐使用将基于 JSON 的连网格式的序列。</span><span class="sxs-lookup"><span data-stu-id="56457-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="56457-180">JSON 是用于表示简单的数据结构以标准文本格式。</span><span class="sxs-lookup"><span data-stu-id="56457-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="56457-181">下面是 JSON 格式的两个 JsonDinner 对象列表如下所示从我们操作方法返回时的示例：</span><span class="sxs-lookup"><span data-stu-id="56457-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="56457-182">调用使用 jQuery 的基于 JSON 的 AJAX 方法</span><span class="sxs-lookup"><span data-stu-id="56457-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="56457-183">现在我们就可以更新用于 SearchController SearchByLocation 操作方法的 NerdDinner 应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="56457-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="56457-184">待办事项，我们将打开 /Views/Home/Index.aspx 视图模板并更新其具有文本框中，搜索按钮，我们映射和&lt;div&gt;名为 dinnerList 元素：</span><span class="sxs-lookup"><span data-stu-id="56457-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="56457-185">然后，我们可以将两个 JavaScript 函数添加到页面：</span><span class="sxs-lookup"><span data-stu-id="56457-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="56457-186">首先加载页面时，第一个 JavaScript 函数加载映射。</span><span class="sxs-lookup"><span data-stu-id="56457-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="56457-187">向上 JavaScript 的第二个 JavaScript 函数连线单击搜索按钮的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="56457-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="56457-188">当按下了按钮它将调用我们将添加到我们的 Map.js 文件的 FindDinnersGivenLocation() JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="56457-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="56457-189">此 FindDinnersGivenLocation() 函数将调用映射。Find （) 上虚拟地球控件中心上输入的位置。</span><span class="sxs-lookup"><span data-stu-id="56457-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="56457-190">当虚拟地球映射服务返回，该映射。Find （） 方法将调用我们作为最后一个参数传递它 callbackUpdateMapDinners 回调方法。</span><span class="sxs-lookup"><span data-stu-id="56457-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="56457-191">CallbackUpdateMapDinners() 方法是这样的实际工作的位置。</span><span class="sxs-lookup"><span data-stu-id="56457-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="56457-192">它使用 jQuery 的 $.post() 帮助器方法来执行 AJAX 调用我们 SearchController SearchByLocation() 操作方法 – 将其传递的纬度和经度新为中心的映射的对象。</span><span class="sxs-lookup"><span data-stu-id="56457-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="56457-193">它定义 $.post() 帮助器方法完成时，将调用一个内联函数，并且从操作方法将传递它使用名为"晚餐"SearchByLocation() 返回 JSON 格式 dinner 结果。</span><span class="sxs-lookup"><span data-stu-id="56457-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="56457-194">然后，它将通过每个返回 dinner 未 foreach 并使用 dinner 的纬度和经度和其他属性图上添加一个新的 pin。</span><span class="sxs-lookup"><span data-stu-id="56457-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="56457-195">它还将 dinner 条目添加到地图右侧晚餐 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="56457-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="56457-196">它然后电线型图钉和 HTML 列表悬停事件，以便当用户悬停在它们上时，将显示有关 dinner 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="56457-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="56457-197">而且，现在我们运行该应用程序并访问主页上我们将看到一幅地图。</span><span class="sxs-lookup"><span data-stu-id="56457-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="56457-198">当我们输入一个市县名称图将显示即将到来晚餐办公电话附近：</span><span class="sxs-lookup"><span data-stu-id="56457-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="56457-199">悬停在 dinner 将显示有关它的详细信息。</span><span class="sxs-lookup"><span data-stu-id="56457-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="56457-200">单击 Dinner 标题在气泡或在 HTML 列表中的右侧将导航我们到 dinner – 我们可以然后 （可选) RSVP 为：</span><span class="sxs-lookup"><span data-stu-id="56457-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="56457-201">下一步</span><span class="sxs-lookup"><span data-stu-id="56457-201">Next Step</span></span>

<span data-ttu-id="56457-202">现在，我们已实施我们 NerdDinner 的应用程序的所有应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="56457-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="56457-203">让我们现在看如何我们可以启用自动单元测试它。</span><span class="sxs-lookup"><span data-stu-id="56457-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56457-204">[上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="56457-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
