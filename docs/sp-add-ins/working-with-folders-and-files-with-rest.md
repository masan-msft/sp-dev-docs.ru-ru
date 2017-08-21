
# <a name="working-with-folders-and-files-with-rest"></a>Работа с папками и файлами в службе REST
Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению (CRUD) папок и файлов с помощью интерфейса REST SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 


 **Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis). 
 


## <a name="working-with-folders-by-using-rest"></a>Работа с папками с помощью REST
<a name="Folders"> </a>

Вы можете получить папку внутри библиотеки документов, если вы знаете ее URL-адрес. Например, вы можете получить корневую папку библиотеки совместно используемых документов с помощью конечной точки, как показано в примере ниже.
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Ниже показан пример свойств папки, которые возвращаются при запрашивании типа контента XML.
 

 



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

В следующем примере показано, как **создать** папку.
 

 



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

В следующем примере показано, как **обновить** папку, используя метод **MERGE**.
 

 



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

В следующем примере показано, как **удалить** папку.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="working-with-files-by-using-rest"></a>Работа с файлами с помощью REST
<a name="Files"> </a>

В приведенном ниже примере показано, как **получить** все файлы из папки.
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В приведенном ниже примере показано, как **получить** определенный файл.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

Вы также можете **получить** файл, если знаете его URL-адрес, как показано в следующем примере.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

В следующем примере показано, как **создать** файл и добавить его в папку.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

В следующем примере показано, как **обновить** файл, используя метод **PUT**.
 

 

 **Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.
 




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

Если вы хотите обновить метаданные файла, необходимо создать конечную точку, которая получает файл как элемент списка. Это возможно, так как каждая папка также является списком, а каждый файл — элементом списка. Создайте такую конечную точку: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  В статье [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest) описано, как обновить метаданные элемента списка.
 

 
Извлеките файл, чтобы никто не смог его изменить, прежде чем вы обновите его. После обновления файл необходимо вернуть, чтобы другие пользователи могли с ним работать. В следующем примере показано, как для **извлечь файл**.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

В следующем примере показано, как для **вернуть файл**.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

В следующем примере показано, как **удалить** файл.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```


## <a name="working-with-large-files-by-using-rest"></a>Работа с большими файлами с помощью REST
<a name="LargeFiles"> </a>

 Отправить двоичный файл больше 1,5 МБ можно только с помощью интерфейса REST. Пример кода для отправки двоичного файла объемом менее 1,5 МБ с помощью объектной модели Javascript SharePoint см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013). Максимальный размер двоичного файла, который можно создать с помощью REST, составляет 2 ГБ. В следующем примере показано, как **создать** большой двоичный файл.
 

 

 **Внимание!** Этот способ работает только в Internet Explorer 10 и последних версиях других браузеров.
 


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

В следующем примере кода показано, как создать файл с помощью этой конечной точки REST и междоменной библиотеки.
 

 



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


## <a name="working-with-files-attached-to-list-items-by-using-rest"></a>Работа с файлами, вложенными в элементы списка, с помощью REST
<a name="FileAttachments"> </a>

В приведенном ниже примере показано, как **получить** все файлы, вложенные в элемент списка.
 

 

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В приведенном ниже примере показано, как **получить** файл, вложенный в элемент списка.
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В следующем примере показано, как **создать** вложение в элемент списка.
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

В следующем примере показано, как **изменить** вложение на элемент списка с помощью метода **PUT**.
 

 

 **Примечание.** Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.
 




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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [Справочные материалы по интерфейсу API службы REST для файлов и папок](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx)
    
 
-  [Отправка файла с помощью REST API и jQuery](upload-a-file-by-using-the-rest-api-and-jquery)
    
 
-  [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest)
    
 
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [SharePoint: выполнение базовых операций доступа к данным файлов и папок с помощью REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
    
 
-  [Выполнение вызовов REST при помощи C# и JavaScript для SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [Выполнение вызовов REST при помощи C# и JavaScript для демоверсии SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint](complete-basic-operations-using-sharepoint-2013-client-library-code)
    
 
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [Разработка надстроек SharePoint](develop-sharepoint-add-ins)
    
 
-  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins)
    
 
-  [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint-2013)
    
 
-  [Open Data Protocol](http://www.odata.org/)
    
 
-  [OData: формат JSON](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
    
 

 

 

