---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 创建 JavaScript 客户端 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 29d50e448e6d282c7db06b9d1946ac221347e1ea
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="create-the-javascript-client"></a><span data-ttu-id="83e3b-102">创建 JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="83e3b-102">Create the JavaScript Client</span></span>
====================
<span data-ttu-id="83e3b-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="83e3b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="83e3b-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="83e3b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="83e3b-105">在本部分中，你将创建客户端应用程序，使用 HTML、 JavaScript 和[Knockout.js](http://knockoutjs.com/)库。</span><span class="sxs-lookup"><span data-stu-id="83e3b-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="83e3b-106">我们将分阶段生成客户端应用程序：</span><span class="sxs-lookup"><span data-stu-id="83e3b-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="83e3b-107">显示的书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="83e3b-107">Showing a list of books.</span></span>
- <span data-ttu-id="83e3b-108">显示簿详细信息。</span><span class="sxs-lookup"><span data-stu-id="83e3b-108">Showing a book detail.</span></span>
- <span data-ttu-id="83e3b-109">添加新书籍。</span><span class="sxs-lookup"><span data-stu-id="83e3b-109">Adding a new book.</span></span>

<span data-ttu-id="83e3b-110">Knockout 库使用模型-视图-视图模型 (MVVM) 模式：</span><span class="sxs-lookup"><span data-stu-id="83e3b-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="83e3b-111">**模型**是服务器端表示形式 （在我们的用例、 丛书和作者） 对业务领域中的数据。</span><span class="sxs-lookup"><span data-stu-id="83e3b-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="83e3b-112">**视图**是表示层 (HTML)。</span><span class="sxs-lookup"><span data-stu-id="83e3b-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="83e3b-113">**视图模型**是包含模型的 JavaScript 对象。</span><span class="sxs-lookup"><span data-stu-id="83e3b-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="83e3b-114">视图模型是 UI 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="83e3b-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="83e3b-115">它具有的 HTML 表示不知道。</span><span class="sxs-lookup"><span data-stu-id="83e3b-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="83e3b-116">相反，它表示抽象功能的视图，如&quot;的书籍的列表&quot;。</span><span class="sxs-lookup"><span data-stu-id="83e3b-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="83e3b-117">视图是数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="83e3b-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="83e3b-118">对视图模型更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="83e3b-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="83e3b-119">视图模型还获取事件从视图中，如按钮单击。</span><span class="sxs-lookup"><span data-stu-id="83e3b-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="83e3b-120">这种方法轻松地更改的布局和 UI 应用程序，因为您可以更改绑定，无需重写任何代码。</span><span class="sxs-lookup"><span data-stu-id="83e3b-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="83e3b-121">例如，可能显示的项作为列表`<ul>`，然后稍后将其更改为表。</span><span class="sxs-lookup"><span data-stu-id="83e3b-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="83e3b-122">添加 Knockout 库</span><span class="sxs-lookup"><span data-stu-id="83e3b-122">Add the Knockout Library</span></span>

<span data-ttu-id="83e3b-123">在 Visual Studio 中，从**工具**菜单上，选择**库程序包管理器**。</span><span class="sxs-lookup"><span data-stu-id="83e3b-123">In Visual Studio, from the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="83e3b-124">然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="83e3b-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="83e3b-125">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="83e3b-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="83e3b-126">此命令将 Knockout 文件添加到脚本文件夹中。</span><span class="sxs-lookup"><span data-stu-id="83e3b-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="83e3b-127">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="83e3b-127">Create the View Model</span></span>

<span data-ttu-id="83e3b-128">添加一个名为脚本文件夹的 app.js 的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="83e3b-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="83e3b-129">(在解决方案资源管理器，右键单击脚本文件夹中，选择**添加**，然后选择**JavaScript 文件**。)粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="83e3b-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="83e3b-130">在 Knockout，`observable`类实现数据绑定。</span><span class="sxs-lookup"><span data-stu-id="83e3b-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="83e3b-131">当可观测对象的内容发生更改时，可观测对象的通知的所有数据绑定控件，以便他们能够更新自己。</span><span class="sxs-lookup"><span data-stu-id="83e3b-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="83e3b-132">(`observableArray`类是数组新版*可观测对象*。)开始时，我们视图模型具有两个可观察对象：</span><span class="sxs-lookup"><span data-stu-id="83e3b-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="83e3b-133">`books` 包含书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="83e3b-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="83e3b-134">`error` 如果 AJAX 调用失败，则包含一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="83e3b-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="83e3b-135">`getAllBooks`方法进行的 AJAX 调用，以便获取的书籍列表。</span><span class="sxs-lookup"><span data-stu-id="83e3b-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="83e3b-136">然后它会推送到结果`books`数组。</span><span class="sxs-lookup"><span data-stu-id="83e3b-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="83e3b-137">`ko.applyBindings`方法是 Knockout 库的一部分。</span><span class="sxs-lookup"><span data-stu-id="83e3b-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="83e3b-138">它采用视图模型作为参数，并将数据绑定设置。</span><span class="sxs-lookup"><span data-stu-id="83e3b-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="83e3b-139">添加脚本捆绑包</span><span class="sxs-lookup"><span data-stu-id="83e3b-139">Add a Script Bundle</span></span>

<span data-ttu-id="83e3b-140">绑定是可以轻松地合并或捆绑到单个文件的多个文件的 ASP.NET 4.5 中的功能。</span><span class="sxs-lookup"><span data-stu-id="83e3b-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="83e3b-141">绑定到服务器，这可以提高页面加载时间减少请求的数。</span><span class="sxs-lookup"><span data-stu-id="83e3b-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="83e3b-142">打开文件应用\_Start/BundleConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="83e3b-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="83e3b-143">将以下代码添加到 RegisterBundles 方法。</span><span class="sxs-lookup"><span data-stu-id="83e3b-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="83e3b-144">[上一页](part-5.md)
> [下一页](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="83e3b-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
