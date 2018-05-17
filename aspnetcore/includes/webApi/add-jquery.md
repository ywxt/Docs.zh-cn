## <a name="call-the-web-api-with-jquery"></a>使用 jQuery 调用 Web API

在本部分中，添加了 HTML 页面使用 jQuery 调用 Web API。 jQuery 启动请求，并用 API 响应中的详细信息更新页面。

配置项目提供静态文件并启用默认文件映射。 通过在 Startup.Configure 中调用 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 和 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 扩展方法完成这一点。 有关详细信息，请参阅[静态文件](xref:fundamentals/static-files)。

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup2.cs?name=snippet_Configure&highlight=3-4)]

将一个名为 index.html 的 HTML 文件添加至项目的 wwwroot 目录。 用以下标记替代其内容：

[!code-html[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/index.html)]

将名为 site.js 的 JavaScript 文件添加至项目的 wwwroot 目录。 用以下代码替代其内容：

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_SiteJs)]

可能需要更改 ASP.NET Core 项目的启动设置，以便对 HTML 页面进行本地测试。 打开项目“属性”目录中的 launchSettings.json。 删除 `launchUrl` 以便在项目的默认文件 index.html 强制打开应用。

有多种方式可以获取 jQuery.。 在前面的代码片段中，库是从 CDN 中加载的。 此示例是一个使用 jQuery 调用 API 的完整 CRUD 示例。 此实例中有很多其他功能可以丰富你的体验。 以下是关于调用 API 的说明。

### <a name="get-a-list-of-to-do-items"></a>获取待办事项的列表

若要获取待办事项列表，请将 HTTP GET 请求发送到 /api/todo。

jQuery [ajax](https://api.jquery.com/jquery.ajax/) 函数将 AJAX 请求发送至 API，这将返回代表对象或数组的 JSON。 此函数可以处理所有形式的 HTTP 交互、将 HTTP 请求发送至指定的 `url`。 `GET` 被用作 `type`。 如果请求成功，则调用 `success` 回调函数。 在该回调中使用待办事项信息更新 DOM。

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_GetData)]

### <a name="add-a-to-do-item"></a>添加待办事项

若要添加代办实现，请将 HTTP POST 请求发送至 /api/todo/。 请求正文应包含待办对象。 [ajax](https://api.jquery.com/jquery.ajax/) 函数使用 `POST` 调用 API。 对于 `POST` 和 `PUT` 请求，请求正文表示发送至 API 的数据。 API 需要 JSON 请求正文。 将 `accepts` 和 `contentType` 设为 `application/json`，以便分别对接收和发送的媒体类型进行分类。 使用 [`JSON.stringify`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 将数据转换为 JSON 对象。 当 API 返回成功状态的代码时，将调用 `getData` 函数来更新 HTML 表。

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AddItem)]

### <a name="update-a-to-do-item"></a>更新待办事项

待办事项的更新与添加非常类似，因为两者都依赖于请求正文。 这种情况下，两者间真正的区别在于添加该项的唯一标识符时会更改 `url`，且 `type` 为 `PUT`。

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AjaxPut)]

### <a name="delete-a-to-do-item"></a>删除待办事项

若要删除待办事项，请将 AJAX 调用上的 `type` 设为 `DELETE` 并指定该项在 URL 中的唯一标识符。

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AjaxDelete)]
