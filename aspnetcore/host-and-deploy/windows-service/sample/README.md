# <a name="custom-webhost-service-sample"></a><span data-ttu-id="193a4-101">自定义 WebHost 服务示例</span><span class="sxs-lookup"><span data-stu-id="193a4-101">Custom WebHost Service Sample</span></span>

<span data-ttu-id="193a4-102">此示例演示而无需使用作为 Windows 服务的 IIS 承载 ASP.NET Core 应用在 Windows 上的推荐的方式。</span><span class="sxs-lookup"><span data-stu-id="193a4-102">This sample shows the recommended way to host an ASP.NET Core app on Windows without using IIS as a Windows Service.</span></span> <span data-ttu-id="193a4-103">此示例演示中所述的功能[ASP.NET Core 应用托管在 Windows 服务](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)。</span><span class="sxs-lookup"><span data-stu-id="193a4-103">This sample demonstrates the features described in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

## <a name="instructions"></a><span data-ttu-id="193a4-104">说明</span><span class="sxs-lookup"><span data-stu-id="193a4-104">Instructions</span></span>

<span data-ttu-id="193a4-105">示例应用程序是一个简单的 MVC web 应用，根据中的说明修改[ASP.NET Core 应用托管在 Windows 服务](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)。</span><span class="sxs-lookup"><span data-stu-id="193a4-105">The sample app is a simple MVC web app modified according to the instructions in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

<span data-ttu-id="193a4-106">若要在服务中运行应用，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="193a4-106">To run the app in a service, perform the following steps:</span></span>

1. <span data-ttu-id="193a4-107">创建在一个文件夹*c:\svc*。</span><span class="sxs-lookup"><span data-stu-id="193a4-107">Create a folder at *c:\svc*.</span></span>

1. <span data-ttu-id="193a4-108">将应用发布到的文件夹`dotnet publish --configuration Release --output c:\\svc`。</span><span class="sxs-lookup"><span data-stu-id="193a4-108">Publish the app to the folder with `dotnet publish --configuration Release --output c:\\svc`.</span></span> <span data-ttu-id="193a4-109">该命令会将应用的资产移动到的文件夹，包括所需`appsettings.json`文件和`wwwroot`文件夹及其内容。</span><span class="sxs-lookup"><span data-stu-id="193a4-109">The command will move the app's assets to the folder, including the required `appsettings.json` file and the `wwwroot` folder with its contents.</span></span>

1. <span data-ttu-id="193a4-110">打开**管理员**命令行界面。</span><span class="sxs-lookup"><span data-stu-id="193a4-110">Open an **administrator** command shell.</span></span>

1. <span data-ttu-id="193a4-111">执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="193a4-111">Execute the following commands:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

1. <span data-ttu-id="193a4-112">在浏览器中，转到`http://localhost:5000`以确认服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="193a4-112">In a browser, go to `http://localhost:5000` to verify that the service is running.</span></span>

1. <span data-ttu-id="193a4-113">若要停止服务，使用该命令：</span><span class="sxs-lookup"><span data-stu-id="193a4-113">To stop the service, use the command:</span></span>

   ```console
   sc stop MyService
   ```

<span data-ttu-id="193a4-114">如果不按预期运行时服务中运行启动应用程序，以使错误消息可访问的捷径是添加日志记录提供程序，如[Windows 事件日志提供程序](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)。</span><span class="sxs-lookup"><span data-stu-id="193a4-114">If the app doesn't start up as expected when running in a service, a quick way to make error messages accessible is to add a logging provider, such as the [Windows EventLog provider](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog).</span></span> <span data-ttu-id="193a4-115">另一种方法是检查系统上使用事件查看器应用程序事件日志。</span><span class="sxs-lookup"><span data-stu-id="193a4-115">Another option is to check the Application Event Log using the Event Viewer on the system.</span></span> <span data-ttu-id="193a4-116">例如，下面是 FileNotFound 错误应用程序事件日志中的未经处理的异常：</span><span class="sxs-lookup"><span data-stu-id="193a4-116">For example, here's an unhandled exception for a FileNotFound error in the Application Event Log:</span></span>

```console
Application: AspNetCoreService.exe
Framework Version: v4.0.30319
Description: The process was terminated due to an unhandled exception.
Exception Info: System.IO.FileNotFoundException
   at Microsoft.Extensions.Configuration.FileConfigurationProvider.Load(Boolean)
   at Microsoft.Extensions.Configuration.ConfigurationRoot..ctor(System.Collections.Generic.IList`1<Microsoft.Extensions.Configuration.IConfigurationProvider>)
   at Microsoft.Extensions.Configuration.ConfigurationBuilder.Build()
   ...
```
