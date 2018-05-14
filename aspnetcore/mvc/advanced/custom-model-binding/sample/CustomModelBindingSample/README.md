# <a name="custom-model-binding-demo"></a>自定义模型绑定演示

通过运行应用并将 base64 编码的字符串发布至 `ImageController` 终结点 (`/api/image/`) 测试 `ByteArrayModelBinder`。 请在请求正文中将文件和文件名属性指定为表单数据（使用 [Postman](https://www.getpostman.com/) 或类似的工具）。 可以使用[本示例字符串](Base64String.txt)。 结果将以指定的文件名保存在 wwwroot/images/upload 文件夹中。

若要测试自定义绑定示例，请尝试以下终结点：

* /api/authors/1
* /api/authors/2（未找到）
* /api/boundauthors/1
* /api/boundauthors/2（未找到）
* /api/boundauthors/get/1
* /api/boundauthors/get/2（无内容）&ndash; 此操作不检查 null，并返回“404 未找到”。
