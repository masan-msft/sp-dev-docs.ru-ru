# <a name="working-with-folders-and-files-with-rest"></a><span data-ttu-id="a4874-101">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="a4874-101">Working with folders and files with REST</span></span>
<span data-ttu-id="a4874-102">Узнайте, как выполнять базовые операции CRUD (создание, чтение, обновление и удаление) с папками и файлами с помощью интерфейса REST в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="a4874-102">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint 2013 REST interface.</span></span>

 <span data-ttu-id="a4874-p101">**Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="a4874-p101">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span> 

## <a name="working-with-folders-by-using-rest"></a><span data-ttu-id="a4874-105">Работа с папками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a4874-105">Working with folders by using REST</span></span>
<span data-ttu-id="a4874-p102"><a name="Folders"> </a> Вы можете получить папку в библиотеке документов, если знаете ее URL-адрес. Например, можно получить корневую папку библиотеки Shared Documents, используя в следующем примере конечную точку.</span><span class="sxs-lookup"><span data-stu-id="a4874-p102"><a name="Folders"> </a> You can retrieve a folder inside a document library when you know its URL. For example, you can retrieve the root folder of your Shared Documents library by using the endpoint in the following example.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="a4874-108">Ниже показан пример свойств папки, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="a4874-108">The following XML shows an example of folder properties that are returned when you request the XML content type.</span></span>

```XML
<content type="application/xml">
<m:properties>
<d:ItemCount m:type="Edm.Int32">0</d:ItemCount>
<d:Name>Shared Documents</d:Name>
<d:ServerRelativeUrl>/Shared Documents</d:ServerRelativeUrl>
<d:WelcomePage/>
</m:properties>
</content>
```
<span data-ttu-id="a4874-109">В следующем примере показано, как **создать** папку.</span><span class="sxs-lookup"><span data-stu-id="a4874-109">The following example shows how to  **create** a folder.</span></span>

```
url: http://site url/_api/web/folders
method: POST
body: { '__metadata': { 'type': 'SP.Folder' }, 'ServerRelativeUrl': '/document library relative url/folder name'}
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="a4874-110">В следующем примере показано, как **обновить** папку, используя метод **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="a4874-110">The following example shows how to  **update** a folder by using the **MERGE** method.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
body: { '__metadata': { 'type': 'SP.Folder' }, 'Name': 'New name' }
Headers: 
     Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="a4874-111">В следующем примере показано, как **удалить** папку.</span><span class="sxs-lookup"><span data-stu-id="a4874-111">The following example shows how to  **delete** a folder.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```
## <a name="working-with-files-by-using-rest"></a><span data-ttu-id="a4874-112">Работа с файлами с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a4874-112">Working with files by using REST</span></span>
<span data-ttu-id="a4874-113"><a name="Files"> </a> В следующем примере показано, как **получить** все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="a4874-113"><a name="Files"> </a> The following example shows how to  **retrieve** all of the files in a folder.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="a4874-114">В следующем примере показано, как **получить** определенный файл.</span><span class="sxs-lookup"><span data-stu-id="a4874-114">The following example shows how to  **retrieve** a specific file.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="a4874-115">Вы также можете **получить** файл, если знаете его URL-адрес, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a4874-115">You can also  **retrieve** a file when you know its URL, as in the following example.</span></span>
 
```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```
<span data-ttu-id="a4874-116">В следующем примере показано, как **создать** файл и добавить его в папку.</span><span class="sxs-lookup"><span data-stu-id="a4874-116">The following example shows how to  **create** a file and add it to a folder.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="a4874-117">В следующем примере показано, как **обновить** файл, используя метод **PUT**.</span><span class="sxs-lookup"><span data-stu-id="a4874-117">The following example shows how to  **update** a file by using the **PUT** method.</span></span>

 <span data-ttu-id="a4874-p103">**Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="a4874-p103">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: POST
body: "Contents of file."
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    X-HTTP-Method:"PUT"
    content-length:length of post body
```
<span data-ttu-id="a4874-p104">Если вы хотите обновить метаданные файла, необходимо создать конечную точку, которая получает файл как элемент списка. Это возможно, так как каждая папка также является списком, а каждый файл — элементом списка. Создайте такую конечную точку: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  В статье [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md) описано, как обновить метаданные элемента списка.</span><span class="sxs-lookup"><span data-stu-id="a4874-p104">If you want to update a file's metadata, you'll have to construct an endpoint that reaches the file as a list item. You can do this because each folder is also a list, and each file is also a list item. Construct an endpoint that looks like this:  `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) explains how to update a list item's metadata.</span></span>
 
<span data-ttu-id="a4874-p105">Извлеките файл, чтобы никто не смог его изменить, прежде чем вы обновите его. После обновления файл необходимо вернуть, чтобы другие пользователи могли с ним работать. В следующем примере показано, как для **извлечь файл**.</span><span class="sxs-lookup"><span data-stu-id="a4874-p105">You may want to check out a file in order to make sure that no one changes it before you update it. After your update, you should also may want to check the file back in so that others can work with it. The following example shows you how to  **check a file out**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```
<span data-ttu-id="a4874-127">В следующем примере показано, как для **вернуть файл**.</span><span class="sxs-lookup"><span data-stu-id="a4874-127">The following example shows you how to  **check a file in**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```
<span data-ttu-id="a4874-128">В следующем примере показано, как **удалить** файл.</span><span class="sxs-lookup"><span data-stu-id="a4874-128">The following example shows how to  **delete** a file.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```

## <a name="working-with-large-files-by-using-rest"></a><span data-ttu-id="a4874-129">Работа с большими файлами с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a4874-129">Working with large files by using REST</span></span>
<span data-ttu-id="a4874-p106"><a name="LargeFiles"> </a> Отправить двоичный файл больше 1,5 МБ можно только с помощью интерфейса REST. Пример кода для отправки двоичного файла объемом менее 1,5 МБ с помощью объектной модели Javascript SharePoint см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013.md). Максимальный размер двоичного файла, который можно создать с помощью REST, составляет 2 ГБ. В следующем примере показано, как **создать** большой двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="a4874-p106"><a name="LargeFiles"> </a> When you need to upload a binary file that is larger than 1.5 megabytes (MB), the REST interface is your only option. See  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013.md) for a code example that shows you how to upload a binary file that is smaller than 1.5 MB by using the SharePoint Javascript object model. The maximum size of a binary file that you can create with REST is 2 gigabytes (GB). The following example shows how to **create** a large binary file.</span></span>
 
 <span data-ttu-id="a4874-134">**Внимание!** Этот способ работает только в Internet Explorer 10 и последних версиях других браузеров.</span><span class="sxs-lookup"><span data-stu-id="a4874-134">**Caution**  This approach will work only with Internet Explorer 10 and the latest versions of other browsers.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/Add(url='file name', overwrite=true)
method: POST
body: contents of binary file
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```
<span data-ttu-id="a4874-135">В следующем примере кода показано, как создать файл с помощью этой конечной точки REST и междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="a4874-135">The following code sample shows how to create a file by using this REST endpoint and the cross-domain library.</span></span>
 
```javascript
function uploadFileBinary() {
XDomainTestHelper.clearLog();
var ro;
if (document.getElementById("TxtViaUrl").value.length > 0) {
ro = new SP.RequestExecutor(document.getElementById("TxtWebUrl").value, document.getElementById("TxtViaUrl").value);
}
else {
ro = new SP.RequestExecutor(document.getElementById("TxtWebUrl").value);
}
var body = "";
for (var i = 0; i < 1000; i++) {
var ch = i % 256;
body = body + String.fromCharCode(ch);
}
var info = {
url: "_api/web/lists/getByTitle('Shared Documents')/RootFolder/Files/Add(url='a.dat', overwrite=true)",
method: "POST",
binaryStringRequestBody: true,
body: body,
success: success,
error: fail,
state: "Update"
};
ro.executeAsync(info);
}

```
## <a name="working-with-files-attached-to-list-items-by-using-rest"></a><span data-ttu-id="a4874-136">Работа со вложенными в элементы списка файлами с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a4874-136">Working with files attached to list items by using REST</span></span>
<span data-ttu-id="a4874-137"><a name="FileAttachments"> </a> В следующем примере показано, как **получить** все файлы, вложенные в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="a4874-137"><a name="FileAttachments"> </a> The following example shows how to  **retrieve** all of the files that are attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
<span data-ttu-id="a4874-138">В следующем примере показано, как **получить** файл, вложенный в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="a4874-138">The following example shows how to  **retrieve** a file that is attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
<span data-ttu-id="a4874-139">В следующем примере показано, как **создать** вложение в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="a4874-139">The following example shows how to  **create** a file attachment to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="a4874-140">В следующем примере показано, как **изменить** вложение на элемент списка с помощью метода **PUT**.</span><span class="sxs-lookup"><span data-stu-id="a4874-140">The following example shows how to  **update** a file attachment to a list item by using the **PUT** method.</span></span>

 <span data-ttu-id="a4874-p107">**Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="a4874-p107">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 
```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: POST
body: "Contents of file."
headers:
    Authorization: "Bearer " + accessToken
    "X-HTTP-Method":"PUT"
    X-RequestDigest: form digest value
    content-length:length of post body
```
## <a name="additional-resources"></a><span data-ttu-id="a4874-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a4874-143">Additional resources</span></span>
<span data-ttu-id="a4874-144"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a4874-144"></span></span>

-  [<span data-ttu-id="a4874-145">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="a4874-145">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="a4874-146">Справочные материалы по интерфейсу API службы REST для файлов и папок</span><span class="sxs-lookup"><span data-stu-id="a4874-146">Files and folders REST API reference</span></span>](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx)
-  [<span data-ttu-id="a4874-147">Отправка файла с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="a4874-147">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery.md)
-  [<span data-ttu-id="a4874-148">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="a4874-148">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="a4874-149">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="a4874-149">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [<span data-ttu-id="a4874-150">SharePoint 2013: выполнение базовых операций с файлами и папками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a4874-150">SharePoint 2013: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [<span data-ttu-id="a4874-151">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="a4874-151">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
-  [<span data-ttu-id="a4874-152">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint 2013 (ролик)</span><span class="sxs-lookup"><span data-stu-id="a4874-152">Making REST calls with C# and JavaScript for SharePoint 2013 demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
-  [<span data-ttu-id="a4874-153">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="a4874-153">Complete basic operations using SharePoint 2013 client library code</span></span>](complete-basic-operations-using-sharepoint-2013-client-library-code.md)
-  [<span data-ttu-id="a4874-154">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="a4874-154">Complete basic operations using JavaScript library code in SharePoint 2013</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013.md)
-  [<span data-ttu-id="a4874-155">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="a4874-155">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
-  [<span data-ttu-id="a4874-156">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="a4874-156">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
-  [<span data-ttu-id="a4874-157">Работа с внешними данными в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="a4874-157">Work with external data in SharePoint 2013</span></span>](work-with-external-data-in-sharepoint-2013.md)
-  [<span data-ttu-id="a4874-158">Протокол OData</span><span class="sxs-lookup"><span data-stu-id="a4874-158">Open Data Protocol</span></span>](http://www.odata.org/)
-  [<span data-ttu-id="a4874-159">OData: формат нотации объектов JavaScript (JSON)</span><span class="sxs-lookup"><span data-stu-id="a4874-159">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
