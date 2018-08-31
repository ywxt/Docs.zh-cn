# <a name="aspnet-core-background-tasks-sample-generic-host"></a>ASP.NET Core 后台任务示例（通用主机）

本示例演示如何使用 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)。 本示例演示了[在 ASP.NET Core 中使用托管服务实现后台任务](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services)主题中描述的功能。

在 [Visual Studio Code](https://code.visualstudio.com/) 中运行示例时，将“.vscode/launch.json”中控制台配置的“控制台”值设置为 `externalTerminal` 或 `integratedTerminal`。 使用 `internalConsole` 与应用对后台工作项进行排队所使用的控制台击键输入不兼容。
