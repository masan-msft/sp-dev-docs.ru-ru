
# <a name="working-with-folders-and-files-with-rest"></a><span data-ttu-id="ba933-101">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="ba933-101">Working with folders and files with REST</span></span>
<span data-ttu-id="ba933-102">Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению (CRUD) папок и файлов с помощью интерфейса REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba933-102">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint REST interface.</span></span>
 

 <span data-ttu-id="ba933-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ba933-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="ba933-p102">**Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis).</span><span class="sxs-lookup"><span data-stu-id="ba933-p102">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis).</span></span> 
 


## <a name="working-with-folders-by-using-rest"></a><span data-ttu-id="ba933-108">Работа с папками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="ba933-108">Working with folders by using REST</span></span>
<span data-ttu-id="ba933-109"><a name="Folders"> </a></span><span class="sxs-lookup"><span data-stu-id="ba933-109"></span></span>

<span data-ttu-id="ba933-p103">Вы можете получить папку внутри библиотеки документов, если вы знаете ее URL-адрес. Например, вы можете получить корневую папку библиотеки совместно используемых документов с помощью конечной точки, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="ba933-p103">You can retrieve a folder inside a document library when you know its URL. For example, you can retrieve the root folder of your Shared Documents library by using the endpoint in the following example.</span></span>
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="ba933-112">Ниже показан пример свойств папки, которые возвращаются при запрашивании типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="ba933-112">The following XML shows an example of folder properties that are returned when you request the XML content type.</span></span>
 

 



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

<span data-ttu-id="ba933-113">В следующем примере показано, как **создать** папку.</span><span class="sxs-lookup"><span data-stu-id="ba933-113">The following example shows how to  **create** a folder.</span></span>
 

 



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

<span data-ttu-id="ba933-114">В следующем примере показано, как **обновить** папку, используя метод **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="ba933-114">The following example shows how to  **update** a folder by using the **MERGE** method.</span></span>
 

 



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

<span data-ttu-id="ba933-115">В следующем примере показано, как **удалить** папку.</span><span class="sxs-lookup"><span data-stu-id="ba933-115">The following example shows how to  **delete** a folder.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="working-with-files-by-using-rest"></a><span data-ttu-id="ba933-116">Работа с файлами с помощью REST</span><span class="sxs-lookup"><span data-stu-id="ba933-116">Working with files by using REST</span></span>
<span data-ttu-id="ba933-117"><a name="Files"> </a></span><span class="sxs-lookup"><span data-stu-id="ba933-117"></span></span>

<span data-ttu-id="ba933-118">В приведенном ниже примере показано, как **получить** все файлы из папки.</span><span class="sxs-lookup"><span data-stu-id="ba933-118">The following example shows how to  **retrieve** all of the files in a folder.</span></span>
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="ba933-119">В приведенном ниже примере показано, как **получить** определенный файл.</span><span class="sxs-lookup"><span data-stu-id="ba933-119">The following example shows how to  **retrieve** a specific file.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="ba933-120">Вы также можете **получить** файл, если знаете его URL-адрес, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ba933-120">You can also  **retrieve** a file when you know its URL, as in the following example.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="ba933-121">В следующем примере показано, как **создать** файл и добавить его в папку.</span><span class="sxs-lookup"><span data-stu-id="ba933-121">The following example shows how to  **create** a file and add it to a folder.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="ba933-122">В следующем примере показано, как **обновить** файл, используя метод **PUT**.</span><span class="sxs-lookup"><span data-stu-id="ba933-122">The following example shows how to  **update** a file by using the **PUT** method.</span></span>
 

 

 <span data-ttu-id="ba933-p104">**Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="ba933-p104">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 




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

<span data-ttu-id="ba933-p105">Если вы хотите обновить метаданные файла, необходимо создать конечную точку, которая получает файл как элемент списка. Это возможно, так как каждая папка также является списком, а каждый файл — элементом списка. Создайте такую конечную точку: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  В статье [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest) описано, как обновить метаданные элемента списка.</span><span class="sxs-lookup"><span data-stu-id="ba933-p105">If you want to update a file's metadata, you'll have to construct an endpoint that reaches the file as a list item. You can do this because each folder is also a list, and each file is also a list item. Construct an endpoint that looks like this:  `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest) explains how to update a list item's metadata.</span></span>
 

 
<span data-ttu-id="ba933-p106">Извлеките файл, чтобы никто не смог его изменить, прежде чем вы обновите его. После обновления файл необходимо вернуть, чтобы другие пользователи могли с ним работать. В следующем примере показано, как для **извлечь файл**.</span><span class="sxs-lookup"><span data-stu-id="ba933-p106">You may want to check out a file in order to make sure that no one changes it before you update it. After your update, you should also may want to check the file back in so that others can work with it. The following example shows you how to  **check a file out**.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<span data-ttu-id="ba933-132">В следующем примере показано, как для **вернуть файл**.</span><span class="sxs-lookup"><span data-stu-id="ba933-132">The following example shows you how to  **check a file in**.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<span data-ttu-id="ba933-133">В следующем примере показано, как **удалить** файл.</span><span class="sxs-lookup"><span data-stu-id="ba933-133">The following example shows how to  **delete** a file.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```


## <a name="working-with-large-files-by-using-rest"></a><span data-ttu-id="ba933-134">Работа с большими файлами с помощью REST</span><span class="sxs-lookup"><span data-stu-id="ba933-134">Working with large files by using REST</span></span>
<span data-ttu-id="ba933-135"><a name="LargeFiles"> </a></span><span class="sxs-lookup"><span data-stu-id="ba933-135"></span></span>

<span data-ttu-id="ba933-p107"> Отправить двоичный файл больше 1,5 МБ можно только с помощью интерфейса REST. Пример кода для отправки двоичного файла объемом менее 1,5 МБ с помощью объектной модели Javascript SharePoint см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013). Максимальный размер двоичного файла, который можно создать с помощью REST, составляет 2 ГБ. В следующем примере показано, как **создать** большой двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="ba933-p107">When you need to upload a binary file that is larger than 1.5 megabytes (MB), the REST interface is your only option. See  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013) for a code example that shows you how to upload a binary file that is smaller than 1.5 MB by using the SharePoint Javascript object model. The maximum size of a binary file that you can create with REST is 2 gigabytes (GB). The following example shows how to **create** a large binary file.</span></span>
 

 

 <span data-ttu-id="ba933-140">**Внимание!** Этот способ работает только в Internet Explorer 10 и последних версиях других браузеров.</span><span class="sxs-lookup"><span data-stu-id="ba933-140">**Caution**  This approach will work only with Internet Explorer 10 and the latest versions of other browsers.</span></span>
 


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

<span data-ttu-id="ba933-141">В следующем примере кода показано, как создать файл с помощью этой конечной точки REST и междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="ba933-141">The following code sample shows how to create a file by using this REST endpoint and the cross-domain library.</span></span>
 

 



```
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


## <a name="working-with-files-attached-to-list-items-by-using-rest"></a><span data-ttu-id="ba933-142">Работа с файлами, вложенными в элементы списка, с помощью REST</span><span class="sxs-lookup"><span data-stu-id="ba933-142">Working with files attached to list items by using REST</span></span>
<span data-ttu-id="ba933-143"><a name="FileAttachments"> </a></span><span class="sxs-lookup"><span data-stu-id="ba933-143"></span></span>

<span data-ttu-id="ba933-144">В приведенном ниже примере показано, как **получить** все файлы, вложенные в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="ba933-144">The following example shows how to  **retrieve** all of the files that are attached to a list item.</span></span>
 

 

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="ba933-145">В приведенном ниже примере показано, как **получить** файл, вложенный в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="ba933-145">The following example shows how to  **retrieve** a file that is attached to a list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="ba933-146">В следующем примере показано, как **создать** вложение в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="ba933-146">The following example shows how to  **create** a file attachment to a list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="ba933-147">В следующем примере показано, как **изменить** вложение на элемент списка с помощью метода **PUT**.</span><span class="sxs-lookup"><span data-stu-id="ba933-147">The following example shows how to  **update** a file attachment to a list item by using the **PUT** method.</span></span>
 

 

 <span data-ttu-id="ba933-p108">**Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="ba933-p108">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 




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


## <a name="additional-resources"></a><span data-ttu-id="ba933-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ba933-150">Additional resources</span></span>
<span data-ttu-id="ba933-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ba933-151"></span></span>


-  [<span data-ttu-id="ba933-152">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="ba933-152">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="ba933-153">Справочные материалы по интерфейсу API службы REST для файлов и папок</span><span class="sxs-lookup"><span data-stu-id="ba933-153">Files and folders REST API reference</span></span>](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="ba933-154">Отправка файла с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="ba933-154">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery)
    
 
-  [<span data-ttu-id="ba933-155">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="ba933-155">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="ba933-156">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="ba933-156">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [<span data-ttu-id="ba933-157">SharePoint: выполнение базовых операций доступа к данным файлов и папок с помощью REST</span><span class="sxs-lookup"><span data-stu-id="ba933-157">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
    
 
-  [<span data-ttu-id="ba933-158">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-158">Making REST calls with C# and JavaScript for SharePoint</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [<span data-ttu-id="ba933-159">Выполнение вызовов REST при помощи C# и JavaScript для демоверсии SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-159">Making REST calls with C# and JavaScript for SharePoint demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [<span data-ttu-id="ba933-160">Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-160">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-2013-client-library-code)
    
 
-  [<span data-ttu-id="ba933-161">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-161">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="ba933-162">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-162">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="ba933-163">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-163">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="ba933-164">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba933-164">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="ba933-165">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="ba933-165">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="ba933-166">OData: формат JSON</span><span class="sxs-lookup"><span data-stu-id="ba933-166">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
    
 

 

 

