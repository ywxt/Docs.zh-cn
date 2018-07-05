---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 创建 JavaScript 客户端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: b0b8ef9bd44bbce5102f2b12717e330f72a9e0c9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400929"
---
<a name="create-the-javascript-client"></a><span data-ttu-id="4fe96-102">创建 JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="4fe96-102">Create the JavaScript Client</span></span>
====================
<span data-ttu-id="4fe96-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4fe96-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4fe96-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="4fe96-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4fe96-105">在本部分中，您将创建使用 HTML、 JavaScript 的客户端应用程序，并[Knockout.js](http://knockoutjs.com/)库。</span><span class="sxs-lookup"><span data-stu-id="4fe96-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="4fe96-106">我们将分阶段构建客户端应用程序：</span><span class="sxs-lookup"><span data-stu-id="4fe96-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="4fe96-107">显示书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="4fe96-107">Showing a list of books.</span></span>
- <span data-ttu-id="4fe96-108">显示某个通讯簿的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4fe96-108">Showing a book detail.</span></span>
- <span data-ttu-id="4fe96-109">添加新书籍。</span><span class="sxs-lookup"><span data-stu-id="4fe96-109">Adding a new book.</span></span>

<span data-ttu-id="4fe96-110">Knockout 库使用模型-视图-视图模型 (MVVM) 模式：</span><span class="sxs-lookup"><span data-stu-id="4fe96-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="4fe96-111">**模型**（在我们的用例、 书籍和作者） 的业务域中的数据的服务器端表示形式。</span><span class="sxs-lookup"><span data-stu-id="4fe96-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="4fe96-112">**视图**是表示层 (HTML)。</span><span class="sxs-lookup"><span data-stu-id="4fe96-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="4fe96-113">**视图模型**是用于保存模型的 JavaScript 对象。</span><span class="sxs-lookup"><span data-stu-id="4fe96-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="4fe96-114">视图模型是在 ui 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="4fe96-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="4fe96-115">它并不知道 HTML 表示形式。</span><span class="sxs-lookup"><span data-stu-id="4fe96-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="4fe96-116">相反，它表示抽象功能的视图，如&quot;书籍列表&quot;。</span><span class="sxs-lookup"><span data-stu-id="4fe96-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="4fe96-117">该视图是数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="4fe96-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="4fe96-118">向视图模型的更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="4fe96-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="4fe96-119">视图模型还获取事件从视图中，如按钮单击。</span><span class="sxs-lookup"><span data-stu-id="4fe96-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="4fe96-120">这种方法轻松更改布局和 UI 的应用，因为您可以更改绑定，无需重新编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="4fe96-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="4fe96-121">例如，可能显示的项作为列表`<ul>`，然后稍后将其更改为一个表。</span><span class="sxs-lookup"><span data-stu-id="4fe96-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="4fe96-122">添加 Knockout 库</span><span class="sxs-lookup"><span data-stu-id="4fe96-122">Add the Knockout Library</span></span>

<span data-ttu-id="4fe96-123">在 Visual Studio 中，从**工具**菜单中，选择**库程序包管理器**。</span><span class="sxs-lookup"><span data-stu-id="4fe96-123">In Visual Studio, from the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="4fe96-124">然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="4fe96-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="4fe96-125">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="4fe96-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="4fe96-126">此命令将 Knockout 文件添加到脚本文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4fe96-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="4fe96-127">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="4fe96-127">Create the View Model</span></span>

<span data-ttu-id="4fe96-128">添加名为脚本文件夹的 app.js 的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="4fe96-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="4fe96-129">(在解决方案资源管理器中右键单击脚本文件夹中，选择**外**，然后选择**JavaScript 文件**。)粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="4fe96-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="4fe96-130">在 Knockout，`observable`类使数据绑定。</span><span class="sxs-lookup"><span data-stu-id="4fe96-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="4fe96-131">当一个可观测对象的内容发生变化时，可观察对象以便他们能够更新本身通知的所有数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="4fe96-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="4fe96-132">(`observableArray`类是数组新版*可观察量*。)开始时，我们的视图模型具有两个可观察量：</span><span class="sxs-lookup"><span data-stu-id="4fe96-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="4fe96-133">`books` 保存书籍列表。</span><span class="sxs-lookup"><span data-stu-id="4fe96-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="4fe96-134">`error` 如果 AJAX 调用失败，则包含一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="4fe96-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="4fe96-135">`getAllBooks`方法通过 AJAX 调用来获取的书籍列表。</span><span class="sxs-lookup"><span data-stu-id="4fe96-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="4fe96-136">然后它会将推送到结果`books`数组。</span><span class="sxs-lookup"><span data-stu-id="4fe96-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="4fe96-137">`ko.applyBindings`方法是 Knockout 库的一部分。</span><span class="sxs-lookup"><span data-stu-id="4fe96-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="4fe96-138">它将作为参数的视图模型，并设置数据绑定。</span><span class="sxs-lookup"><span data-stu-id="4fe96-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="4fe96-139">添加脚本捆绑包</span><span class="sxs-lookup"><span data-stu-id="4fe96-139">Add a Script Bundle</span></span>

<span data-ttu-id="4fe96-140">捆绑是一项功能 ASP.NET 4.5，轻松地组合或多个文件捆绑到一个文件中。</span><span class="sxs-lookup"><span data-stu-id="4fe96-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="4fe96-141">绑定可以请求数减少到服务器，这可以提高页面加载时间。</span><span class="sxs-lookup"><span data-stu-id="4fe96-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="4fe96-142">打开文件应用\_Start/BundleConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="4fe96-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="4fe96-143">将以下代码添加到 RegisterBundles 方法。</span><span class="sxs-lookup"><span data-stu-id="4fe96-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="4fe96-144">[上一页](part-5.md)
> [下一页](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="4fe96-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
