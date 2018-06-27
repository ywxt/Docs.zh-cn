# <a name="custom-webhost-service-sample"></a>自定义 WebHost 服务示例

本示例演示如何在不使用 IIS 的情况下将 ASP.NET Core 应用作为 Windows 服务进行托管。 本示例演示[在 Windows 服务中托管 ASP.NET Core 应用](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)中描述的方案。

## <a name="instructions"></a>说明

示例应用是一个根据[在 Windows 服务中托管 ASP.NET Core 应用](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)中的说明修改的 Razor Pages Web 应用。

若要在服务中运行应用，请执行下列步骤：

1. 在 c:\svc 下创建文件夹。

1. 将应用发布到带有 `dotnet publish --configuration Release --output c:\\svc` 的文件夹。 该命令会将应用的资产移至 svc 文件夹，包括必需的 `appsettings.json` 文件和 `wwwroot` 文件夹。

1. 打开管理员命令提示符。

1. 执行以下命令：

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

  等于号和路径字符串的开头之间需要添加空格。

1. 在浏览器中，导航到 `http://localhost:5000` 并验证服务正在运行。 应用将重定向到安全终结点 `https://localhost:5001`。

1. 要停止服务，请使用以下命令：

   ```console
   sc stop MyService
   ```

如果应用未按预期方式启动，则可以访问错误消息的快速方法是添加日志记录提供程序，例如 [Windows EventLog 提供程序](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)。 另一种方法是使用系统上的事件查看器来检查应用程序事件日志。 例如，下面是应用程序事件日志中 FileNotFound 错误的未经处理的异常：

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
