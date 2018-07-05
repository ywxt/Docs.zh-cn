默认模板创建“RazorPagesMovie”、“主页”、“关于”和“联系人”链接和页面。 可能需要单击导航图标才能显示这些链接，具体取决于浏览器窗口的大小。

![主页或索引页](~/tutorials/razor-pages/razor-pages-start/_static/home2.png)

测试链接。 “RazorPagesMovie”和“主页”链接转到“索引”页。 “关于”和“联系人”链接分别转到 `About` 和 `Contact` 页面。

## <a name="project-files-and-folders"></a>项目文件和文件夹

下表列出了项目中的文件和文件夹。 对于本教程而言，Startup.cs 是最有必要了解的文件。 无需查看下面提供的每一个链接。 需要详细了解项目中的某个文件或文件夹时，可参考此处提供的链接。

| 文件或文件夹 | 目标 |
| -------------- | ------- |
| *wwwroot* | 包含静态资产。 请参阅[静态文件](xref:fundamentals/static-files)。 |
| *页* | [Razor Pages](xref:razor-pages/index)的文件夹。 |
| *appsettings.json* | [配置](xref:fundamentals/configuration/index) |
| *Program.cs* | 配置 ASP.NET Core 应用的[主机](xref:fundamentals/host/index)。 |
| *Startup.cs* | 配置服务和请求管道。 请参阅[启动](xref:fundamentals/startup)。 |

### <a name="the-pagesshared-folder"></a>Pages/Shared 文件夹

_Layout.cshtml 文件包含常见的 HTML 元素（脚本和样式表链接），并设置应用的布局。 例如，如果选择“RazorPagesMovie”、“主页”、“关于”或“联系人”，则网页中会出现一组常见的元素。 常见的元素包括顶部的导航菜单和窗口底部的标题。 请参阅[布局](xref:mvc/views/layout)以了解详细信息。

_ValidationScriptsPartial.cshtml 文件提供对 [jQuery](https://jquery.com/) 验证脚本的引用。 在本教程的后续部分中添加 `Create` 和 `Edit` 页面时，会使用 _ValidationScriptsPartial.cshtml 文件。

_CookieConsentPartial.cshtml 文件提供了导航栏以及用于汇总隐私和 cookie 使用策略的目录。 若要详细了解该项目中包含的 GDPR 资产，请参阅 [ASP.NET Core 中的欧盟一般数据保护条例 (GDPR) 支持](xref:security/gdpr)。

### <a name="the-pages-folder"></a>“页面”文件夹

*_ViewStart.cshtml*将 Razor Pages `Layout` 属性设置为使用 *_Layout.cshtml* 文件。 请参阅[布局](xref:mvc/views/layout)了解详细信息。

_ViewImports.cshtml 文件包含要导入每个 Razor 页面的 Razor 指令。 请参阅[导入共享指令](xref:mvc/views/layout#importing-shared-directives)了解详细信息。

`About`、`Contact` 和 `Index` 页面是基本页面，可用于启动应用。 `Error` 页面用于显示错误信息。
