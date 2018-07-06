---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |Microsoft Docs
author: microsoft
description: 步骤 12 显示了如何开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 2247dc2e6d22cc0d5ddba97dfe6c7d2d1b0e49be
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819401"
---
<a name="enable-automated-unit-testing"></a><span data-ttu-id="9fdf2-103">启用自动单元测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-103">Enable Automated Unit Testing</span></span>
====================
<span data-ttu-id="9fdf2-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9fdf2-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9fdf2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="9fdf2-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="9fdf2-106">这是一种免费的步骤 12 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-106">This is step 12 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="9fdf2-107">步骤 12 显示了如何开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改和对应用程序在将来的改进。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-107">Step 12 shows how to develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>
> 
> <span data-ttu-id="9fdf2-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-12-unit-testing"></a><span data-ttu-id="9fdf2-109">NerdDinner 步骤 12： 单元测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-109">NerdDinner Step 12: Unit Testing</span></span>

<span data-ttu-id="9fdf2-110">让我们来开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改和对应用程序在将来的改进。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-110">Let's develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>

### <a name="why-unit-test"></a><span data-ttu-id="9fdf2-111">为什么单元测试？</span><span class="sxs-lookup"><span data-stu-id="9fdf2-111">Why Unit Test?</span></span>

<span data-ttu-id="9fdf2-112">在工作一天早上的驱动器上可以启发您正在使用的应用程序突然立刻正式投入工作。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-112">On the drive into work one morning you have a sudden flash of inspiration about an application you are working on.</span></span> <span data-ttu-id="9fdf2-113">您意识到可以实现的更改，可让应用程序极大的改进。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-113">You realize there is a change you can implement that will make the application dramatically better.</span></span> <span data-ttu-id="9fdf2-114">它可能是一个重构的清理代码中，添加一个新功能或修复 bug。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-114">It might be a refactoring that cleans up the code, adds a new feature, or fixes a bug.</span></span>

<span data-ttu-id="9fdf2-115">Confronts，当您在您的计算机的问题-"安全是它，使这一改进？"</span><span class="sxs-lookup"><span data-stu-id="9fdf2-115">The question that confronts you when you arrive at your computer is – "how safe is it to make this improvement?"</span></span> <span data-ttu-id="9fdf2-116">如果在更改具有副作用或中断的内容？</span><span class="sxs-lookup"><span data-stu-id="9fdf2-116">What if making the change has side effects or breaks something?</span></span> <span data-ttu-id="9fdf2-117">更改可能很简单，只需几分钟才能实现，但如果需要手动测试的应用程序方案的所有小时？</span><span class="sxs-lookup"><span data-stu-id="9fdf2-117">The change might be simple and only take a few minutes to implement, but what if it takes hours to manually test out all of the application scenarios?</span></span> <span data-ttu-id="9fdf2-118">如果忘记方案和损坏的应用程序进入成品阶段？</span><span class="sxs-lookup"><span data-stu-id="9fdf2-118">What if you forget to cover a scenario and a broken application goes into production?</span></span> <span data-ttu-id="9fdf2-119">正在进行此项改进真的值得下的所有工作？</span><span class="sxs-lookup"><span data-stu-id="9fdf2-119">Is making this improvement really worth all the effort?</span></span>

<span data-ttu-id="9fdf2-120">自动化的单元测试可以提供网络安全，使您能够不断改进您的应用程序，并避免害怕正在处理的代码。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-120">Automated unit tests can provide a safety net that enables you to continually enhance your applications, and avoid being afraid of the code you are working on.</span></span> <span data-ttu-id="9fdf2-121">具有自动快速验证功能，可以使用置信度 – 代码，使您可以进行改进可能否则不具有的感觉舒适的测试执行。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-121">Having automated tests that quickly verify functionality enables you to code with confidence – and empower you to make improvements you might otherwise not have felt comfortable doing.</span></span> <span data-ttu-id="9fdf2-122">它们还帮助创建更易于维护的解决方案，并让较长的生存期的到高得多的潜在客户的投资回报。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-122">They also help create solutions that are more maintainable and have a longer lifetime - which leads to a much higher return on investment.</span></span>

<span data-ttu-id="9fdf2-123">ASP.NET MVC 框架可以简单而自然到单元测试应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-123">The ASP.NET MVC Framework makes it easy and natural to unit test application functionality.</span></span> <span data-ttu-id="9fdf2-124">它还使支持测试优先的基于的开发的测试驱动开发 (TDD) 工作流。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-124">It also enables a Test Driven Development (TDD) workflow that enables test-first based development.</span></span>

### <a name="nerddinnertests-project"></a><span data-ttu-id="9fdf2-125">NerdDinner.Tests 项目</span><span class="sxs-lookup"><span data-stu-id="9fdf2-125">NerdDinner.Tests Project</span></span>

<span data-ttu-id="9fdf2-126">我们在本教程开头创建了 NerdDinner 应用程序，我们已收到一个提示对话框询问我们是否想要创建单元测试项目随附的应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-126">When we created our NerdDinner application at the beginning of this tutorial, we were prompted with a dialog asking whether we wanted to create a unit test project to go along with the application project:</span></span>

![](enable-automated-unit-testing/_static/image1.png)

<span data-ttu-id="9fdf2-127">我们保留"是的创建单元测试项目"单选按钮处于选中状态 – 这将导致"NerdDinner.Tests"项目添加到我们的解决方案：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-127">We kept the "Yes, create a unit test project" radio button selected – which resulted in a "NerdDinner.Tests" project being added to our solution:</span></span>

![](enable-automated-unit-testing/_static/image2.png)

<span data-ttu-id="9fdf2-128">NerdDinner.Tests 项目引用 NerdDinner 应用程序项目程序集，并使我们能够轻松地将自动的测试添加到其验证应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-128">The NerdDinner.Tests project references the NerdDinner application project assembly, and enables us to easily add automated tests to it that verify the application functionality.</span></span>

### <a name="creating-unit-tests-for-our-dinner-model-class"></a><span data-ttu-id="9fdf2-129">为我们 Dinner Model 类创建单元测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-129">Creating Unit Tests for our Dinner Model Class</span></span>

<span data-ttu-id="9fdf2-130">让我们将一些测试添加到验证我们创建当我们构建我们的模型层的 Dinner 类我们 NerdDinner.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-130">Let's add some tests to our NerdDinner.Tests project that verify the Dinner class we created when we built our model layer.</span></span>

<span data-ttu-id="9fdf2-131">我们将首先创建模型相关的测试，我们将放置我们名为"Models"的测试项目的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-131">We'll start by creating a new folder within our test project called "Models" where we'll place our model-related tests.</span></span> <span data-ttu-id="9fdf2-132">我们然后右键单击文件夹并选择**Add-&gt;新的测试**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-132">We'll then right-click on the folder and choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="9fdf2-133">这将显示"添加新测试"对话框。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-133">This will bring up the "Add New Test" dialog.</span></span>

<span data-ttu-id="9fdf2-134">我们将选择要创建一个"单元测试"并将其命名为"DinnerTest.cs":</span><span class="sxs-lookup"><span data-stu-id="9fdf2-134">We'll choose to create a "Unit Test" and name it "DinnerTest.cs":</span></span>

![](enable-automated-unit-testing/_static/image3.png)

<span data-ttu-id="9fdf2-135">当我们单击"确定"按钮时 Visual Studio 将添加 （和打开） DinnerTest.cs 文件到项目：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-135">When we click the "ok" button Visual Studio will add (and open) a DinnerTest.cs file to the project:</span></span>

![](enable-automated-unit-testing/_static/image4.png)

<span data-ttu-id="9fdf2-136">默认 Visual Studio 单元测试模板有大量的样板代码在其中找到略为凌乱。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-136">The default Visual Studio unit test template has a bunch of boiler-plate code within it that I find a little messy.</span></span> <span data-ttu-id="9fdf2-137">让我们把它整理出来以只包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-137">Let's clean it up to just contain the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

<span data-ttu-id="9fdf2-138">在上面的 DinnerTest 类 [TestClass] 属性将其识别为测试，以及可选的测试初始化和拆卸代码将包含的类。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-138">The [TestClass] attribute on the DinnerTest class above identifies it as a class that will contain tests, as well as optional test initialization and teardown code.</span></span> <span data-ttu-id="9fdf2-139">我们可以通过添加 [TestMethod] 特性对它们的公共方法来定义在其中测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-139">We can define tests within it by adding public methods that have a [TestMethod] attribute on them.</span></span>

<span data-ttu-id="9fdf2-140">下面是我们将添加的两个执行我们的 Dinner 类测试的第一个。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-140">Below are the first of two tests we'll add that exercise our Dinner class.</span></span> <span data-ttu-id="9fdf2-141">第一个测试将验证我们 Dinner 无效，是否创建新的 Dinner 时没有正确设置所有属性。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-141">The first test verifies that our Dinner is invalid if a new Dinner is created without all properties being set correctly.</span></span> <span data-ttu-id="9fdf2-142">第二个测试验证我们 Dinner Dinner 具有所有属性都设置使用有效的值时有效：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-142">The second test verifies that our Dinner is valid when a Dinner has all properties set with valid values:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

<span data-ttu-id="9fdf2-143">您会注意到上面我们测试名称都是非常明确的 （并且却稍微有些繁琐的）。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-143">You'll notice above that our test names are very explicit (and somewhat verbose).</span></span> <span data-ttu-id="9fdf2-144">因为我们最终可能会创建数百或数千个小测试，并且我们想要轻松地快速确定意向和每个行为 （尤其是在我们正在通过测试运行程序中的失败的列表），我们将执行此操作。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-144">We are doing this because we might end up creating hundreds or thousands of small tests, and we want to make it easy to quickly determine the intent and behavior of each of them (especially when we are looking through a list of failures in a test runner).</span></span> <span data-ttu-id="9fdf2-145">测试名称应以命名要测试的功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-145">The test names should be named after the functionality they are testing.</span></span> <span data-ttu-id="9fdf2-146">我们使用更高版本"名词\_应\_谓词"命名模式。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-146">Above we are using a "Noun\_Should\_Verb" naming pattern.</span></span>

<span data-ttu-id="9fdf2-147">我们构建的测试使用测试模式 –"Arrange，Act，Assert"代表"AAA":</span><span class="sxs-lookup"><span data-stu-id="9fdf2-147">We are structuring the tests using the "AAA" testing pattern – which stands for "Arrange, Act, Assert":</span></span>

- <span data-ttu-id="9fdf2-148">排列： 设置要测试的单元</span><span class="sxs-lookup"><span data-stu-id="9fdf2-148">Arrange: Setup the unit being tested</span></span>
- <span data-ttu-id="9fdf2-149">Act： 执行测试的单元，并捕获结果</span><span class="sxs-lookup"><span data-stu-id="9fdf2-149">Act: Exercise the unit under test and capture results</span></span>
- <span data-ttu-id="9fdf2-150">断言： 验证行为</span><span class="sxs-lookup"><span data-stu-id="9fdf2-150">Assert: Verify the behavior</span></span>

<span data-ttu-id="9fdf2-151">当我们编写时我们想要避免的各个测试的测试执行过多操作。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-151">When we write tests we want to avoid having the individual tests do too much.</span></span> <span data-ttu-id="9fdf2-152">而是每个测试应验证仅在一个概念 （这将使其更易于找出失败的原因）。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-152">Instead each test should verify only a single concept (which will make it much easier to pinpoint the cause of failures).</span></span> <span data-ttu-id="9fdf2-153">比较好的原则是尝试，且只能包含一个断言语句为每个测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-153">A good guideline is to try and only have a single assert statement for each test.</span></span> <span data-ttu-id="9fdf2-154">如果你有多个断言测试方法中的语句，请确保它们都被用于测试相同的概念。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-154">If you have more than one assert statement in a test method, make sure they are all being used to test the same concept.</span></span> <span data-ttu-id="9fdf2-155">如有疑问，请另一个测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-155">When in doubt, make another test.</span></span>

### <a name="running-tests"></a><span data-ttu-id="9fdf2-156">正在运行测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-156">Running Tests</span></span>

<span data-ttu-id="9fdf2-157">Visual Studio 2008 Professional （和更高版本） 包括可用于运行 Visual Studio 单元测试项目在 IDE 中的内置测试运行程序。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-157">Visual Studio 2008 Professional (and higher editions) includes a built-in test runner that can be used to run Visual Studio Unit Test projects within the IDE.</span></span> <span data-ttu-id="9fdf2-158">我们可以选择**测试-&gt;运行-&gt;解决方案中的所有测试**菜单命令 （或类型 Ctrl R、 A） 若要运行所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-158">We can select the **Test-&gt;Run-&gt;All Tests in Solution** menu command (or type Ctrl R, A) to run all of our unit tests.</span></span> <span data-ttu-id="9fdf2-159">或或者我们可以在特定的测试类或测试方法中我们光标的位置，并使用**测试-&gt;运行-&gt;当前上下文中的测试**菜单命令 （或类型 Ctrl R、 T） 运行的单元测试的子集。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-159">Or alternatively we can position our cursor within a specific test class or test method and use the **Test-&gt;Run-&gt;Tests in Current Context** menu command (or type Ctrl R, T) to run a subset of the unit tests.</span></span>

<span data-ttu-id="9fdf2-160">让我们 DinnerTest 类中的我们光标的位置并键入"Ctrl R、 T"到我们刚才定义的运行这两个测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-160">Let's position our cursor within the DinnerTest class and type "Ctrl R, T" to run the two tests we just defined.</span></span> <span data-ttu-id="9fdf2-161">当我们执行此操作的"测试结果"窗口将显示在 Visual Studio 中，我们将看到我们测试运行中列出的结果：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-161">When we do this a "Test Results" window will appear within Visual Studio and we'll see the results of our test run listed within it:</span></span>

![](enable-automated-unit-testing/_static/image5.png)

<span data-ttu-id="9fdf2-162">*注意： VS 测试结果窗口不默认情况下显示的类名称列。可以通过在测试结果窗口内右键单击并使用添加/删除列菜单命令添加此。*</span><span class="sxs-lookup"><span data-stu-id="9fdf2-162">*Note: The VS test results window does not show the Class Name column by default. You can add this by right-clicking within the Test Results window and using the Add/Remove Columns menu command.*</span></span>

<span data-ttu-id="9fdf2-163">我们的两个测试中花费了只有一小部分第二个运行，并为您可以在这两种传递，请参阅。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-163">Our two tests took only a fraction of a second to run – and as you can see they both passed.</span></span> <span data-ttu-id="9fdf2-164">我们现在可以继续并通过它们来创建其他测试，验证特定的规则验证，以及涵盖两个帮助器方法-IsUserHost() 和 IsUserRegisterd() – 我们添加到 Dinner 类扩充。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-164">We can now go on and augment them by creating additional tests that verify specific rule validations, as well as cover the two helper methods - IsUserHost() and IsUserRegisterd() – that we added to the Dinner class.</span></span> <span data-ttu-id="9fdf2-165">将所有这些测试放在 Dinner 类的位置将使其更容易且更安全，若要向其在将来添加新的业务规则和验证。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-165">Having all these tests in place for the Dinner class will make it much easier and safer to add new business rules and validations to it in the future.</span></span> <span data-ttu-id="9fdf2-166">我们可以将我们新的规则逻辑添加到 Dinner，然后秒内验证它没有破坏任何我们以前的逻辑功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-166">We can add our new rule logic to Dinner, and then within seconds verify that it hasn't broken any of our previous logic functionality.</span></span>

<span data-ttu-id="9fdf2-167">请注意如何使用描述性的测试名称轻松地快速了解每个测试验证。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-167">Notice how using a descriptive test name makes it easy to quickly understand what each test is verifying.</span></span> <span data-ttu-id="9fdf2-168">我建议使用**工具-&gt;选项**菜单命令，打开的测试工具-&gt;测试执行配置屏幕中，并检查"双击已失败或无结论的单元测试结果显示测试失败的点"复选框。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-168">I recommend using the **Tools-&gt;Options** menu command, opening the Test Tools-&gt;Test Execution configuration screen, and checking the "Double-clicking a failed or inconclusive unit test result displays the point of failure in the test" checkbox.</span></span> <span data-ttu-id="9fdf2-169">这样，您可以双击测试结果窗口中的故障，立即跳转到断言失败。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-169">This will allow you to double-click on a failure in the test results window and jump immediately to the assert failure.</span></span>

### <a name="creating-dinnerscontroller-unit-tests"></a><span data-ttu-id="9fdf2-170">创建 DinnersController 的单元测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-170">Creating DinnersController Unit Tests</span></span>

<span data-ttu-id="9fdf2-171">让我们现在创建验证我们 DinnersController 的功能的一些单元测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-171">Let's now create some unit tests that verify our DinnersController functionality.</span></span> <span data-ttu-id="9fdf2-172">我们将首先右键单击测试项目中的"控制器"文件夹，然后选择**Add-&gt;新的测试**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-172">We'll start by right-clicking on the "Controllers" folder within our Test project and then choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="9fdf2-173">我们将创建一个"单元测试"并将其命名为"DinnersControllerTest.cs"。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-173">We'll create a "Unit Test" and name it "DinnersControllerTest.cs".</span></span>

<span data-ttu-id="9fdf2-174">我们将创建两个验证 DinnersController 的 Details() 操作方法的测试方法。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-174">We'll create two test methods that verify the Details() action method on the DinnersController.</span></span> <span data-ttu-id="9fdf2-175">第一个将验证现有 Dinner 请求时，返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-175">The first will verify that a View is returned when an existing Dinner is requested.</span></span> <span data-ttu-id="9fdf2-176">第二个将验证不存在 Dinner 请求时，返回"NotFound"视图：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-176">The second will verify that a "NotFound" view is returned when a non-existent Dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

<span data-ttu-id="9fdf2-177">上面的代码将编译成清理。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-177">The above code compiles clean.</span></span> <span data-ttu-id="9fdf2-178">当我们运行测试时，不过，它们都失败：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-178">When we run the tests, though, they both fail:</span></span>

![](enable-automated-unit-testing/_static/image6.png)

<span data-ttu-id="9fdf2-179">如果我们看一下错误消息，我们会看到测试失败的原因是因为我们 DinnersRepository 类无法连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-179">If we look at the error messages, we'll see that the reason the tests failed was because our DinnersRepository class was unable to connect to a database.</span></span> <span data-ttu-id="9fdf2-180">我们 NerdDinner 应用程序到本地 SQL Server Express 文件存在于 \App 下使用连接字符串\_NerdDinner 应用程序项目的数据目录。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-180">Our NerdDinner application is using a connection-string to a local SQL Server Express file which lives under the \App\_Data directory of the NerdDinner application project.</span></span> <span data-ttu-id="9fdf2-181">因为我们 NerdDinner.Tests 项目编译和运行在不同的目录中然后应用程序项目，我们连接字符串的相对路径位置不正确。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-181">Because our NerdDinner.Tests project compiles and runs in a different directory then the application project, the relative path location of our connection-string is incorrect.</span></span>

<span data-ttu-id="9fdf2-182">我们*无法*通过将 SQL Express 数据库文件复制到我们的测试项目，修复此问题，然后向其中添加了适当测试的连接字符串，我们的测试项目的 App.config 中。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-182">We *could* fix this by copying the SQL Express database file to our test project, and then add an appropriate test connection-string to it in the App.config of our test project.</span></span> <span data-ttu-id="9fdf2-183">此参数将被解除阻止，并运行上述测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-183">This would get the above tests unblocked and running.</span></span>

<span data-ttu-id="9fdf2-184">单元测试代码中使用的实际数据库，不过，带来了许多挑战。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-184">Unit testing code using a real database, though, brings with it a number of challenges.</span></span> <span data-ttu-id="9fdf2-185">尤其是在下列情况下：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-185">Specifically:</span></span>

- <span data-ttu-id="9fdf2-186">会显著降低的单元测试执行时间。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-186">It significantly slows down the execution time of unit tests.</span></span> <span data-ttu-id="9fdf2-187">它所花费的时间来运行测试，频繁地执行它们的可能性越小。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-187">The longer it takes to run tests, the less likely you are to execute them frequently.</span></span> <span data-ttu-id="9fdf2-188">理想情况下，您希望单元测试，以能够在数秒内 – 运行并将其作为内容的自然作为编译项目。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-188">Ideally you want your unit tests to be able to be run in seconds – and have it be something you do as naturally as compiling the project.</span></span>
- <span data-ttu-id="9fdf2-189">在测试中的设置和清理逻辑比较复杂。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-189">It complicates the setup and cleanup logic within tests.</span></span> <span data-ttu-id="9fdf2-190">您希望每个单元测试是独立的、 独立于其他人 （不带任何副作用或依赖项）。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-190">You want each unit test to be isolated and independent of others (with no side effects or dependencies).</span></span> <span data-ttu-id="9fdf2-191">实际数据库上运行时需要注意的状态和测试之间将它重置。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-191">When working against a real database you have to be mindful of state and reset it between tests.</span></span>

<span data-ttu-id="9fdf2-192">让我们看一下名为"依赖关系注入"，可帮助我们解决这些问题，并避免与我们的测试中使用的实际数据库的需求的设计模式。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-192">Let's look at a design pattern called "dependency injection" that can help us work around these issues and avoid the need to use a real database with our tests.</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="9fdf2-193">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="9fdf2-193">Dependency Injection</span></span>

<span data-ttu-id="9fdf2-194">稍后再试 DinnersController"与紧密耦合"DinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-194">Right now DinnersController is tightly "coupled" to the DinnerRepository class.</span></span> <span data-ttu-id="9fdf2-195">"耦合"是指在其中一个类显式依赖于另一个类才能正常工作的情况：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-195">"Coupling" refers to a situation where a class explicitly relies on another class in order to work:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

<span data-ttu-id="9fdf2-196">由于 DinnerRepository 类需要对数据库的访问，紧密耦合的依赖关系 DinnersController 类具有 DinnerRepository 两端需要我们要测试的 DinnersController 操作方法的顺序中有一个数据库。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-196">Because the DinnerRepository class requires access to a database, the tightly coupled dependency the DinnersController class has on the DinnerRepository ends up requiring us to have a database in order for the DinnersController action methods to be tested.</span></span>

<span data-ttu-id="9fdf2-197">通过使用称为"依赖关系注入"– 这是一种方法在其中依赖项 （如提供数据访问的存储库类） 不再隐式创建中使用它们的类的设计模式，我们可以获得解决此问题。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-197">We can get around this by employing a design pattern called "dependency injection" – which is an approach where dependencies (like repository classes that provide data access) are no longer implicitly created within classes that use them.</span></span> <span data-ttu-id="9fdf2-198">而是依赖项可以显式传递给使用它们的类使用构造函数自变量。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-198">Instead, dependencies can be explicitly passed to the class that uses them using constructor arguments.</span></span> <span data-ttu-id="9fdf2-199">如果使用接口定义了依赖项，然后，我们可以灵活地在单元测试方案的"假"的依赖项实现中传递。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-199">If the dependencies are defined using interfaces, we then have the flexibility to pass in "fake" dependency implementations for unit test scenarios.</span></span> <span data-ttu-id="9fdf2-200">这让我们来创建实际上并不要求对数据库的访问的特定于测试的依赖项实现。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-200">This enables us to create test-specific dependency implementations that do not actually require access to a database.</span></span>

<span data-ttu-id="9fdf2-201">若要了解此操作，让我们来实现与我们 DinnersController 的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-201">To see this in action, let's implement dependency injection with our DinnersController.</span></span>

#### <a name="extracting-an-idinnerrepository-interface"></a><span data-ttu-id="9fdf2-202">提取 IDinnerRepository 接口</span><span class="sxs-lookup"><span data-stu-id="9fdf2-202">Extracting an IDinnerRepository interface</span></span>

<span data-ttu-id="9fdf2-203">我们第一步将创建新的 IDinnerRepository 接口封装我们控制器要求以检索和更新 Dinners 的存储库协定。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-203">Our first step will be to create a new IDinnerRepository interface that encapsulates the repository contract our controllers require to retrieve and update Dinners.</span></span>

<span data-ttu-id="9fdf2-204">我们可以通过右键单击 \Models 文件夹，然后选择手动定义此接口协定**Add-&gt;新项**菜单命令，并创建名为 IDinnerRepository.cs 新接口。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-204">We can define this interface contract manually by right-clicking on the \Models folder, and then choosing the **Add-&gt;New Item** menu command and creating a new interface named IDinnerRepository.cs.</span></span>

<span data-ttu-id="9fdf2-205">或者我们可以使用重构工具内置于 Visual Studio Professional （和更高版本） 自动提取，并为我们创建一个接口，从我们现有的 DinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-205">Alternatively we can use the refactoring tools built-into Visual Studio Professional (and higher editions) to automatically extract and create an interface for us from our existing DinnerRepository class.</span></span> <span data-ttu-id="9fdf2-206">若要提取使用与此接口，只需将光标置于 DinnerRepository 类中，在文本编辑器，然后右键单击并选择**重构-&gt;提取接口**菜单命令：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-206">To extract this interface using VS, simply position the cursor in the text editor on the DinnerRepository class, and then right-click and choose the **Refactor-&gt;Extract Interface** menu command:</span></span>

![](enable-automated-unit-testing/_static/image7.png)

<span data-ttu-id="9fdf2-207">这将启动"提取接口"对话框并提示我们输入要创建的接口的名称。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-207">This will launch the "Extract Interface" dialog and prompt us for the name of the interface to create.</span></span> <span data-ttu-id="9fdf2-208">它将默认为 IDinnerRepository 并自动选择要添加到接口的现有 DinnerRepository 类上的所有公共方法：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-208">It will default to IDinnerRepository and automatically select all public methods on the existing DinnerRepository class to add to the interface:</span></span>

![](enable-automated-unit-testing/_static/image8.png)

<span data-ttu-id="9fdf2-209">当我们单击"确定"按钮时，Visual Studio 会将新 IDinnerRepository 接口添加到我们的应用程序：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-209">When we click the "ok" button, Visual Studio will add a new IDinnerRepository interface to our application:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

<span data-ttu-id="9fdf2-210">并将更新我们现有的 DinnerRepository 类，以便它实现该接口：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-210">And our existing DinnerRepository class will be updated so that it implements the interface:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a><span data-ttu-id="9fdf2-211">正在更新 DinnersController 以支持构造函数注入</span><span class="sxs-lookup"><span data-stu-id="9fdf2-211">Updating DinnersController to support constructor injection</span></span>

<span data-ttu-id="9fdf2-212">现在，我们将更新要使用的新界面的 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-212">We'll now update the DinnersController class to use the new interface.</span></span>

<span data-ttu-id="9fdf2-213">当前 DinnersController 已经过硬编码，以便其"dinnerRepository"字段始终是 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-213">Currently DinnersController is hard-coded such that its "dinnerRepository" field is always a DinnerRepository class:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

<span data-ttu-id="9fdf2-214">我们将更改它，以便"dinnerRepository"字段的类型而不是 DinnerRepository IDinnerRepository 是。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-214">We'll change it so that the "dinnerRepository" field is of type IDinnerRepository instead of DinnerRepository.</span></span> <span data-ttu-id="9fdf2-215">然后，我们将添加两个公共 DinnersController 构造函数。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-215">We'll then add two public DinnersController constructors.</span></span> <span data-ttu-id="9fdf2-216">一个构造函数允许将 IDinnerRepository 作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-216">One of the constructors allows an IDinnerRepository to be passed as an argument.</span></span> <span data-ttu-id="9fdf2-217">另一个是使用我们现有的 DinnerRepository 实现的默认构造函数：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-217">The other is a default constructor that uses our existing DinnerRepository implementation:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

<span data-ttu-id="9fdf2-218">由于默认情况下的 ASP.NET MVC 创建控制器类使用默认构造函数，在运行时我们 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-218">Because ASP.NET MVC by default creates controller classes using default constructors, our DinnersController at runtime will continue to use the DinnerRepository class to perform data access.</span></span>

<span data-ttu-id="9fdf2-219">我们现在可以更新单元测试，不过，在"假"dinner 存储库实现中使用参数的构造函数传递。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-219">We can now update our unit tests, though, to pass in a "fake" dinner repository implementation using the parameter constructor.</span></span> <span data-ttu-id="9fdf2-220">此"假"dinner 存储库将不需要访问的实际数据库，而将使用内存中示例数据。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-220">This "fake" dinner repository will not require access to a real database, and instead will use in-memory sample data.</span></span>

#### <a name="creating-the-fakedinnerrepository-class"></a><span data-ttu-id="9fdf2-221">创建 FakeDinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="9fdf2-221">Creating the FakeDinnerRepository class</span></span>

<span data-ttu-id="9fdf2-222">让我们创建 FakeDinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-222">Let's create a FakeDinnerRepository class.</span></span>

<span data-ttu-id="9fdf2-223">我们将首先创建我们 NerdDinner.Tests 项目中的"Fakes"目录，然后向其中添加新的 FakeDinnerRepository 类 (右键单击文件夹并选择**Add-&gt;的新类**):</span><span class="sxs-lookup"><span data-stu-id="9fdf2-223">We'll begin by creating a "Fakes" directory within our NerdDinner.Tests project and then add a new FakeDinnerRepository class to it (right-click on the folder and choose **Add-&gt;New Class**):</span></span>

![](enable-automated-unit-testing/_static/image9.png)

<span data-ttu-id="9fdf2-224">我们将更新代码，以便 FakeDinnerRepository 类实现 IDinnerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-224">We'll update the code so that the FakeDinnerRepository class implements the IDinnerRepository interface.</span></span> <span data-ttu-id="9fdf2-225">然后，我们可以右键单击它，并选择"实现接口 IDinnerRepository"上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-225">We can then right-click on it and choose the "Implement interface IDinnerRepository" context menu command:</span></span>

![](enable-automated-unit-testing/_static/image10.png)

<span data-ttu-id="9fdf2-226">这会导致 Visual Studio 会自动将所有 IDinnerRepository 接口成员添加到"存根"的默认实现我们 FakeDinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-226">This will cause Visual Studio to automatically add all of the IDinnerRepository interface members to our FakeDinnerRepository class with default "stub out" implementations:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

<span data-ttu-id="9fdf2-227">我们然后可以更新 FakeDinnerRepository 实现，以便从内存中列表&lt;Dinner&gt;集合作为构造函数参数传递给它：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-227">We can then update the FakeDinnerRepository implementation to work off of an in-memory List&lt;Dinner&gt; collection passed to it as a constructor argument:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

<span data-ttu-id="9fdf2-228">现在，我们不需要数据库，并且可以改为脱离 Dinner 对象的内存中列表的虚设 IDinnerRepository 实现。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-228">We now have a fake IDinnerRepository implementation that does not require a database, and can instead work off an in-memory list of Dinner objects.</span></span>

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a><span data-ttu-id="9fdf2-229">对单元测试使用 FakeDinnerRepository</span><span class="sxs-lookup"><span data-stu-id="9fdf2-229">Using the FakeDinnerRepository with Unit Tests</span></span>

<span data-ttu-id="9fdf2-230">让我们返回到之前失败，因为该数据库不可用的 DinnersController 单元测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-230">Let's return to the DinnersController unit tests that failed earlier because the database wasn't available.</span></span> <span data-ttu-id="9fdf2-231">我们可以更新测试方法，用于填充向 DinnersController 使用下面的代码示例中内存 Dinner 数据 FakeDinnerRepository:</span><span class="sxs-lookup"><span data-stu-id="9fdf2-231">We can update the test methods to use a FakeDinnerRepository populated with sample in-memory Dinner data to the DinnersController using the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

<span data-ttu-id="9fdf2-232">和现在当我们运行这些测试都通过：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-232">And now when we run these tests they both pass:</span></span>

![](enable-automated-unit-testing/_static/image11.png)

<span data-ttu-id="9fdf2-233">最重要的是，它们需要只有一小部分第二个运行，并且不需要任何复杂的安装程序清理逻辑。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-233">Best of all, they take only a fraction of a second to run, and do not require any complicated setup/cleanup logic.</span></span> <span data-ttu-id="9fdf2-234">我们可以现在单元测试所有我们 DinnersController 操作方法的代码 （包括列表中，分页的详细信息，创建、 更新和删除），而根本无需连接到真实的数据库。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-234">We can now unit test all of our DinnersController action method code (including listing, paging, details, create, update and delete) without ever needing to connect to a real database.</span></span>

| <span data-ttu-id="9fdf2-235">**端主题： 依赖关系注入框架**</span><span class="sxs-lookup"><span data-stu-id="9fdf2-235">**Side Topic: Dependency Injection Frameworks**</span></span> |
| --- |
| <span data-ttu-id="9fdf2-236">执行手动依赖关系注入 （例如，我们是上面） 可正常使用，但会变成难以维护作为依赖项的数量并提高应用程序中的组件。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-236">Performing manual dependency injection (like we are above) works fine, but does become harder to maintain as the number of dependencies and components in an application increases.</span></span> <span data-ttu-id="9fdf2-237">为有助于提供更多的依赖关系管理灵活性的.NET 而存在多个依赖关系注入框架。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-237">Several dependency injection frameworks exist for .NET that can help provide even more dependency management flexibility.</span></span> <span data-ttu-id="9fdf2-238">这些框架，有时也称为"控制反转"(IoC) 容器，提供机制，以使一层额外的配置对指定并将依赖项传递给对象在运行时 （通常使用构造函数注入的支持).</span><span class="sxs-lookup"><span data-stu-id="9fdf2-238">These frameworks, also sometimes called "Inversion of Control" (IoC) containers, provide mechanisms that enable an additional level of configuration support for specifying and passing dependencies to objects at runtime (most often using constructor injection).</span></span> <span data-ttu-id="9fdf2-239">一些更受欢迎的 OSS 依赖关系注入 / IOC 框架在.NET 中的包括： AutoFac、 Ninject、 Spring.NET、 StructureMap 和 Windsor。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-239">Some of the more popular OSS Dependency Injection / IOC frameworks in .NET include: AutoFac, Ninject, Spring.NET, StructureMap, and Windsor.</span></span> <span data-ttu-id="9fdf2-240">ASP.NET MVC 公开扩展性 Api，允许开发人员参与的解决方法和实例化控制器，并可让依赖关系注入 / IoC 框架完全集成此进程中。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-240">ASP.NET MVC exposes extensibility APIs that enable developers to participate in the resolution and instantiation of controllers, and which enables Dependency Injection / IoC frameworks to be cleanly integrated within this process.</span></span> <span data-ttu-id="9fdf2-241">使用 DI/IOC 框架还会使我们能够从我们 DinnersController – 将完全删除它和 DinnerRepositorys 之间的耦合删除默认构造函数。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-241">Using a DI/IOC framework would also enable us to remove the default constructor from our DinnersController – which would completely remove the coupling between it and the DinnerRepositorys.</span></span> <span data-ttu-id="9fdf2-242">我们不会使用依赖关系注入 / IOC 框架与 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-242">We won't be using a dependency injection / IOC framework with our NerdDinner application.</span></span> <span data-ttu-id="9fdf2-243">但是，这是一个我们可以考虑在将来，如果 NerdDinner 基本代码和功能的大小增长。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-243">But it is something we could consider for the future if the NerdDinner code-base and capabilities grew.</span></span> |

### <a name="creating-edit-action-unit-tests"></a><span data-ttu-id="9fdf2-244">创建编辑操作单元测试</span><span class="sxs-lookup"><span data-stu-id="9fdf2-244">Creating Edit Action Unit Tests</span></span>

<span data-ttu-id="9fdf2-245">让我们现在创建一些单元测试以确认 DinnersController 的编辑功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-245">Let's now create some unit tests that verify the Edit functionality of the DinnersController.</span></span> <span data-ttu-id="9fdf2-246">我们首先测试我们的编辑操作的 HTTP GET 版本：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-246">We'll start by testing the HTTP-GET version of our Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

<span data-ttu-id="9fdf2-247">我们将创建一个测试，以便验证时请求有效 dinner 呈现由 DinnerFormViewModel 对象支持的视图：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-247">We'll create a test that verifies that a View backed by a DinnerFormViewModel object is rendered back when a valid dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

<span data-ttu-id="9fdf2-248">当我们运行测试时，不过，我们会发现失败，因为时编辑方法访问 User.Identity.Name 属性执行 Dinner.IsHostedBy() 检查将引发空引用异常。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-248">When we run the test, though, we'll find that it fails because a null reference exception is thrown when the Edit method accesses the User.Identity.Name property to perform the Dinner.IsHostedBy() check.</span></span>

<span data-ttu-id="9fdf2-249">控制器基类上的用户对象封装有关登录的用户的详细信息，并在运行时创建控制器时，由 ASP.NET MVC 填充。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-249">The User object on the Controller base class encapsulates details about the logged-in user, and is populated by ASP.NET MVC when it creates the controller at runtime.</span></span> <span data-ttu-id="9fdf2-250">因为我们要测试 web 服务器环境外部 DinnersController，未设置用户对象 （因此导致 null 引用异常）。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-250">Because we are testing the DinnersController outside of a web-server environment, the User object isn't set (hence the null reference exception).</span></span>

### <a name="mocking-the-useridentityname-property"></a><span data-ttu-id="9fdf2-251">模拟 User.Identity.Name 属性</span><span class="sxs-lookup"><span data-stu-id="9fdf2-251">Mocking the User.Identity.Name property</span></span>

<span data-ttu-id="9fdf2-252">模拟框架使测试变得更容易通过使我们能够动态创建虚设支持我们的测试中的依赖对象的版本。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-252">Mocking frameworks make testing easier by enabling us to dynamically create fake versions of dependent objects that support our tests.</span></span> <span data-ttu-id="9fdf2-253">例如，我们可以在我们的编辑操作测试使用的模拟框架，动态创建我们 DinnersController 可用于查找模拟的用户名的用户对象。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-253">For example, we can use a mocking framework in our Edit action test to dynamically create a User object that our DinnersController can use to lookup a simulated username.</span></span> <span data-ttu-id="9fdf2-254">这可以避免当我们运行测试时引发空引用。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-254">This will avoid a null reference from being thrown when we run our test.</span></span>

<span data-ttu-id="9fdf2-255">有很多.NET 模拟可与 ASP.NET MVC 框架 (见下面这些设置的列表： [ http://www.mockframeworks.com/ ](http://www.mockframeworks.com/))。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-255">There are many .NET mocking frameworks that can be used with ASP.NET MVC (you can see a list of them here: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)).</span></span> <span data-ttu-id="9fdf2-256">为了测试我们将使用一种开放源模拟框架名为"Moq"我们 NerdDinner 应用程序，这可以免费从下载[ http://www.mockframeworks.com/moq ](http://www.mockframeworks.com/moq)。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-256">For testing our NerdDinner application we'll use an open source mocking framework called "Moq", which can be downloaded for free from [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).</span></span>

<span data-ttu-id="9fdf2-257">下载完成后，我们将对 Moq.dll 程序集 NerdDinner.Tests 项目中添加的引用：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-257">Once downloaded, we'll add a reference in our NerdDinner.Tests project to the Moq.dll assembly:</span></span>

![](enable-automated-unit-testing/_static/image12.png)

<span data-ttu-id="9fdf2-258">然后，我们将添加一个"CreateDinnersControllerAs(username)"帮助器方法为我们的测试类的用户名将作为参数，哪些则"模拟"DinnersController 实例上的 User.Identity.Name 属性：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-258">We'll then add a "CreateDinnersControllerAs(username)" helper method to our test class that takes a username as a parameter, and which then "mocks" the User.Identity.Name property on the DinnersController instance:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

<span data-ttu-id="9fdf2-259">更高版本，我们将使用 Moq 创建 fakes 的 ControllerContext 对象 （这是什么 ASP.NET MVC 将传递到控制器类，以公开运行时对象，如用户、 请求、 响应和会话） 的模拟对象。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-259">Above we are using Moq to create a Mock object that fakes a ControllerContext object (which is what ASP.NET MVC passes to Controller classes to expose runtime objects like User, Request, Response, and Session).</span></span> <span data-ttu-id="9fdf2-260">我们在模拟来指示的 ControllerContext HttpContext.User.Identity.Name 属性应返回我们传递给帮助器方法的用户名字符串上调用"SetupGet"方法。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-260">We are calling the "SetupGet" method on the Mock to indicate that the HttpContext.User.Identity.Name property on ControllerContext should return the username string we passed to the helper method.</span></span>

<span data-ttu-id="9fdf2-261">我们可以模拟任意数量的 ControllerContext 属性和方法。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-261">We can mock any number of ControllerContext properties and methods.</span></span> <span data-ttu-id="9fdf2-262">为了说明这一点我还添加了 SetupGet() 调用 Request.IsAuthenticated 属性 （这不实际所需的下面 – 的测试，但这有助于解释如何可以模拟请求属性）。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-262">To illustrate this I've also added a SetupGet() call for the Request.IsAuthenticated property (which isn't actually needed for the tests below – but which helps illustrate how you can mock Request properties).</span></span> <span data-ttu-id="9fdf2-263">当我们完成我们的 ControllerContext 模拟的一个实例分配向 DinnersController 我们帮助器方法返回。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-263">When we are done we assign an instance of the ControllerContext mock to the DinnersController our helper method returns.</span></span>

<span data-ttu-id="9fdf2-264">我们现在可以编写使用此帮助器方法来测试编辑方案涉及不同的用户的单元测试：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-264">We can now write unit tests that use this helper method to test Edit scenarios involving different users:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

<span data-ttu-id="9fdf2-265">现在当我们运行测试时传递：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-265">And now when we run the tests they pass:</span></span>

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a><span data-ttu-id="9fdf2-266">测试 UpdateModel() 方案</span><span class="sxs-lookup"><span data-stu-id="9fdf2-266">Testing UpdateModel() scenarios</span></span>

<span data-ttu-id="9fdf2-267">我们创建了测试以涵盖编辑操作的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-267">We've created tests that cover the HTTP-GET version of the Edit action.</span></span> <span data-ttu-id="9fdf2-268">让我们现在创建某些编辑操作的 HTTP POST 版本验证测试：</span><span class="sxs-lookup"><span data-stu-id="9fdf2-268">Let's now create some tests that verify the HTTP-POST version of the Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

<span data-ttu-id="9fdf2-269">有关我们支持与此操作方法的有趣的新测试方案是控制器基类上的 UpdateModel() 帮助器方法的用法。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-269">The interesting new testing scenario for us to support with this action method is its usage of the UpdateModel() helper method on the Controller base class.</span></span> <span data-ttu-id="9fdf2-270">我们将使用此帮助器方法来将窗体发布值绑定到 Dinner 对象实例。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-270">We are using this helper method to bind form-post values to our Dinner object instance.</span></span>

<span data-ttu-id="9fdf2-271">下面是演示，我们可以如何提供窗体发布 UpdateModel() 帮助器方法，若要使用的值的两个测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-271">Below are two tests that demonstrates how we can supply form posted values for the UpdateModel() helper method to use.</span></span> <span data-ttu-id="9fdf2-272">我们将通过创建和填充 FormCollection 对象执行此操作，然后将其分配给在控制器上的"ValueProvider"属性。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-272">We'll do this by creating and populating a FormCollection object, and then assign it to the "ValueProvider" property on the Controller.</span></span>

<span data-ttu-id="9fdf2-273">第一个测试验证，成功保存将浏览器重定向到详细信息的操作。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-273">The first test verifies that on a successful save the browser is redirected to the details action.</span></span> <span data-ttu-id="9fdf2-274">第二个测试将验证发送无效的输入时该操作显示编辑视图再次使用一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-274">The second test verifies that when invalid input is posted the action redisplays the edit view again with an error message.</span></span>


[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a><span data-ttu-id="9fdf2-275">测试总结</span><span class="sxs-lookup"><span data-stu-id="9fdf2-275">Testing Wrap-Up</span></span>

<span data-ttu-id="9fdf2-276">我们已经介绍了在单元测试控制器类中所涉及的核心概念。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-276">We've covered the core concepts involved in unit testing controller classes.</span></span> <span data-ttu-id="9fdf2-277">我们可以使用这些技术可以轻松地创建数百个简单的测试，验证我们的应用程序的行为。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-277">We can use these techniques to easily create hundreds of simple tests that verify the behavior of our application.</span></span>

<span data-ttu-id="9fdf2-278">我们的控制器和模型的测试不需要的实际数据库，因为它们是极其快速且轻松地运行。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-278">Because our controller and model tests do not require a real database, they are extremely fast and easy to run.</span></span> <span data-ttu-id="9fdf2-279">我们将能够在数秒内，执行数百个自动测试并立即获取我们所做的更改是否中断的内容的反馈。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-279">We'll be able to execute hundreds of automated tests in seconds, and immediately get feedback as to whether a change we made broke something.</span></span> <span data-ttu-id="9fdf2-280">这将有助于向我们提供的置信度来持续改进，重构，并改进我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-280">This will help provide us the confidence to continually improve, refactor, and refine our application.</span></span>

<span data-ttu-id="9fdf2-281">我们介绍如何测试作为最后一个主题中这一章 – 但不是因为测试是应在开发过程结束时执行 ！</span><span class="sxs-lookup"><span data-stu-id="9fdf2-281">We covered testing as the last topic in this chapter – but not because testing is something you should do at the end of a development process!</span></span> <span data-ttu-id="9fdf2-282">相反，应在开发过程中尽早编写自动的测试。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-282">On the contrary, you should write automated tests as early as possible in your development process.</span></span> <span data-ttu-id="9fdf2-283">这样做因此可以立即获得反馈开发时，可帮助你仔细考虑应用程序的用例场景，并会引导您设计应用程序分层和记住耦合干净。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-283">Doing so enables you to get immediate feedback as you develop, helps you think thoughtfully about your application's use case scenarios, and guides you to design your application with clean layering and coupling in mind.</span></span>

<span data-ttu-id="9fdf2-284">本书中的更高版本的章节将讨论测试驱动开发 (TDD) 以及如何使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-284">A later chapter in the book will discuss Test Driven Development (TDD), and how to use it with ASP.NET MVC.</span></span> <span data-ttu-id="9fdf2-285">首先编写的测试，都能满足你生成的代码，TDD 也迭代的编码实践。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-285">TDD is an iterative coding practice where you first write the tests that your resulting code will satisfy.</span></span> <span data-ttu-id="9fdf2-286">与 TDD 开始每项功能通过创建一个测试，以便验证您将要实现的功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-286">With TDD you begin each feature by creating a test that verifies the functionality you are about to implement.</span></span> <span data-ttu-id="9fdf2-287">编写单元测试第一次可帮助确保你清楚地了解此功能，如何它应该适用。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-287">Writing the unit test first helps ensure that you clearly understand the feature and how it is supposed to work.</span></span> <span data-ttu-id="9fdf2-288">仅编写该测试 （并已验证它失败后） 然后实现此测试将验证的实际功能。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-288">Only after the test is written (and you have verified that it fails) do you then implement the actual functionality the test verifies.</span></span> <span data-ttu-id="9fdf2-289">因为您已经花了时间思考的功能是怎样工作的用例，你将具有更好地了解要求和如何最好地实现它们。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-289">Because you've already spent time thinking about the use case of how the feature is supposed to work, you will have a better understanding of the requirements and how best to implement them.</span></span> <span data-ttu-id="9fdf2-290">完成您可以重新运行测试 – 并立即获得反馈的实现时是否功能能够正常运行。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-290">When you are done with the implementation you can re-run the test – and get immediate feedback as to whether the feature works correctly.</span></span> <span data-ttu-id="9fdf2-291">我们将介绍第 10 章中更 TDD。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-291">We'll cover TDD more in Chapter 10.</span></span>

### <a name="next-step"></a><span data-ttu-id="9fdf2-292">下一步</span><span class="sxs-lookup"><span data-stu-id="9fdf2-292">Next Step</span></span>

<span data-ttu-id="9fdf2-293">一些最后一个注释总结。</span><span class="sxs-lookup"><span data-stu-id="9fdf2-293">Some final wrap up comments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9fdf2-294">[上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)</span><span class="sxs-lookup"><span data-stu-id="9fdf2-294">[Previous](use-ajax-to-implement-mapping-scenarios.md)
[Next](nerddinner-wrap-up.md)</span></span>
