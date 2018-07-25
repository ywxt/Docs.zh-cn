# <a name="cookie-sharing-sample-app"></a>Cookie 共享示例应用

此示例演示了在使用 cookie 身份验证的三个应用之间共享 cookie:

| 项目                             | 描述 |
| ----------------------------------- | ----------- |
| CookieAuth.Core                     | ASP.NET Core Razor 页面应用，而无需使用 ASP.NET Core 标识 |
| CookieAuthWithIdentity.Core         | 使用 ASP.NET Core 标识的 ASP.NET Core MVC 应用程序 |
| CookieAuthWithIdentity.NETFramework | 使用 ASP.NET 标识的 ASP.NET Framework MVC 应用程序 |

说明：

1. 运行 CookieAuth.Core 应用。 注册用户。 应用程序对用户进行身份验证时注册该用户。 注销用户。
1. 在同一浏览器会话中，运行 CookieAuthWithIdentity.Core 应用。 将同一用户注册为与核心应用程序一起使用。 应用程序对用户进行身份验证时注册该用户。 注销用户。
1. 在同一浏览器会话中，运行 CookieAuthWithIdentity.NETFramework 应用。 将同一用户注册为使用与其他应用程序。 应用程序对用户进行身份验证时注册该用户。 注销用户。
1. 登录到三个应用的任何用户。 在应用之间共享身份验证 cookie。 请注意，用户会自动登录到其他两个应用。
1. 注销用户从任何应用。 请注意用户自动注销的其他两个应用。

此示例演示中所述的功能[应用之间共享 cookie](https://docs.microsoft.com/aspnet/core/security/cookie-sharing)主题。
