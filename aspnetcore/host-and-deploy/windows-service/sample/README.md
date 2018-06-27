# <a name="custom-webhost-service-sample"></a><span data-ttu-id="db9db-101">自定义 WebHost 服务示例</span><span class="sxs-lookup"><span data-stu-id="db9db-101">Custom WebHost Service Sample</span></span>

<span data-ttu-id="db9db-102">本示例演示如何在不使用 IIS 的情况下将 ASP.NET Core 应用作为 Windows 服务进行托管。</span><span class="sxs-lookup"><span data-stu-id="db9db-102">This sample shows how to host an ASP.NET Core app as a Windows Service without using IIS.</span></span> <span data-ttu-id="db9db-103">本示例演示[在 Windows 服务中托管 ASP.NET Core 应用](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)中描述的方案。</span><span class="sxs-lookup"><span data-stu-id="db9db-103">This sample demonstrates the scenario described in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

## <a name="instructions"></a><span data-ttu-id="db9db-104">说明</span><span class="sxs-lookup"><span data-stu-id="db9db-104">Instructions</span></span>

<span data-ttu-id="db9db-105">示例应用是一个根据[在 Windows 服务中托管 ASP.NET Core 应用](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)中的说明修改的 Razor Pages Web 应用。</span><span class="sxs-lookup"><span data-stu-id="db9db-105">The sample app is a Razor Pages web app modified according to the instructions in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

<span data-ttu-id="db9db-106">若要在服务中运行应用，请执行下列步骤：</span><span class="sxs-lookup"><span data-stu-id="db9db-106">To run the app in a service, perform the following steps:</span></span>

1. <span data-ttu-id="db9db-107">在 c:\svc 下创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="db9db-107">Create a folder at *c:\svc*.</span></span>

1. <span data-ttu-id="db9db-108">将应用发布到带有 `dotnet publish --configuration Release --output c:\\svc` 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="db9db-108">Publish the app to the folder with `dotnet publish --configuration Release --output c:\\svc`.</span></span> <span data-ttu-id="db9db-109">该命令会将应用的资产移至 svc 文件夹，包括必需的 `appsettings.json` 文件和 `wwwroot` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="db9db-109">The command moves the app's assets to the *svc* folder, including the required `appsettings.json` file and the `wwwroot` folder.</span></span>

1. <span data-ttu-id="db9db-110">打开管理员命令提示符。</span><span class="sxs-lookup"><span data-stu-id="db9db-110">Open an **administrator** command prompt.</span></span>

1. <span data-ttu-id="db9db-111">执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="db9db-111">Execute the following commands:</span></span>

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

  <span data-ttu-id="db9db-112">等于号和路径字符串的开头之间需要添加空格。</span><span class="sxs-lookup"><span data-stu-id="db9db-112">*The space between the equal sign and the start of the path string is required.*</span></span>

1. <span data-ttu-id="db9db-113">在浏览器中，导航到 `http://localhost:5000` 并验证服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="db9db-113">In a browser, navigate to `http://localhost:5000` and verify that the service is running.</span></span> <span data-ttu-id="db9db-114">应用将重定向到安全终结点 `https://localhost:5001`。</span><span class="sxs-lookup"><span data-stu-id="db9db-114">The app redirects to the secure endpoint `https://localhost:5001`.</span></span>

1. <span data-ttu-id="db9db-115">要停止服务，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="db9db-115">To stop the service, use the command:</span></span>

   ```console
   sc stop MyService
   ```

<span data-ttu-id="db9db-116">如果应用未按预期方式启动，则可以访问错误消息的快速方法是添加日志记录提供程序，例如 [Windows EventLog 提供程序](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)。</span><span class="sxs-lookup"><span data-stu-id="db9db-116">If the app doesn't start as expected, a quick way to make error messages accessible is to add a logging provider, such as the [Windows EventLog provider](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog).</span></span> <span data-ttu-id="db9db-117">另一种方法是使用系统上的事件查看器来检查应用程序事件日志。</span><span class="sxs-lookup"><span data-stu-id="db9db-117">Another option is to check the Application Event Log using the Event Viewer on the system.</span></span> <span data-ttu-id="db9db-118">例如，下面是应用程序事件日志中 FileNotFound 错误的未经处理的异常：</span><span class="sxs-lookup"><span data-stu-id="db9db-118">For example, here's an unhandled exception for a FileNotFound error in the Application Event Log:</span></span>

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
