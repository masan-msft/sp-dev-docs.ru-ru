---
title: "Работа с папками и файлами в службе REST"
description: "Выполнение основных операций по созданию, чтению, обновлению и удалению папок и файлов с помощью интерфейса REST SharePoint."
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: f440fc48cccc5ea573889b4f2a04cfb125ac3b78
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="working-with-folders-and-files-with-rest"></a>Работа с папками и файлами в службе REST

> [!TIP] 
> Служба REST SharePoint Online (а также локальной среды SharePoint 2016 и более поздних версий) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData `$batch`. Дополнительные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md). 

<a name="Folders"> </a>

## <a name="working-with-folders-by-using-rest"></a>Работа с папками при помощи REST

Вы можете получить папку внутри библиотеки документов, если вы знаете ее URL-адрес. Например, вы можете получить корневую папку библиотеки совместно используемых документов с помощью конечной точки, как показано в примере ниже.


```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

Ниже показан пример свойств папки, которые возвращаются при запросе типа контента XML.

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

<br/>

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

<br/>

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

<br/>

В приведенном ниже примере показано, как **удалить** папку.

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

<br/>

<a name="Files"> </a>

## <a name="working-with-files-by-using-rest"></a>Работа с файлами при помощи REST

В приведенном ниже примере показано, как **получить** все файлы в папке.

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

В следующем примере показано, как **получить** конкретный файл.

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<br/>

Вы также можете **получить** файл, если вы знаете его URL-адрес, как показано в примере ниже.

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<br/>

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

<br/>

В следующем примере показано, как **обновить** файл, используя метод **PUT**.
 
> [!NOTE] 
> Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.

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

<br/>

Если вы хотите обновить метаданные файла, необходимо создать конечную точку, которая получает файл как элемент списка. Это возможно, так как каждая папка также является списком, а каждый файл — элементом списка. Создайте такую конечную точку: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`. Информацию о том, как обновить метаданные элемента списка, см. в статье [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md). 

Извлеките файл, чтобы никто не смог его изменить, прежде чем вы обновите его. После обновления файл необходимо вернуть, чтобы другие пользователи могли с ним работать. В приведенном ниже примере показано, как **извлечь файл**.

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<br/>

В приведенном ниже примере показано, как **вернуть файл**.

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<br/>

В приведенном ниже примере показано, как **удалить** файл.

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```

<br/>

<a name="LargeFiles"> </a>

## <a name="working-with-large-files-by-using-rest"></a>Работа с большими файлами при помощи REST

Отправить двоичный файл размером более 1,5 МБ можно только с помощью интерфейса REST. Пример кода для отправки двоичного файла размером менее 1,5 МБ с помощью объектной модели JavaScript SharePoint см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md). Максимальный размер двоичного файла, который можно создать с помощью REST, составляет 2 ГБ. В приведенном ниже примере показано, как **создать** большой двоичный файл.
 
> [!WARNING] 
> Этот способ работает только в Internet Explorer 10 и последних версиях других браузеров.

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

<br/>

В приведенном ниже примере кода показано, как создать файл с помощью этой конечной точки REST и междоменной библиотеки.

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

<br/>

<a name="FileAttachments"> </a>

## <a name="working-with-files-attached-to-list-items-by-using-rest"></a>Работа со вложенными в элементы списка файлами при помощи REST


В приведенном ниже примере показано, как **получить** все файлы, вложенные в элемент списка.

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

В следующем примере показано, как **извлечь** файл, подключенный к элементу списка.

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

В следующем примере показано, как **создать** подключение файла к элементу списка.

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

<br/>

В приведенном ниже примере показано, как **заменить** вложенный файл на элемент списка с помощью метода **PUT**.
 
> [!NOTE] 
> Обновлять файлы можно только с помощью метода **PUT**. Использовать метод **MERGE** запрещено.

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

<br/>

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md)   
- [Справочные материалы по REST API и примеры](https://msdn.microsoft.com/library)
- [Отправка файла с помощью REST API и jQuery](upload-a-file-by-using-the-rest-api-and-jquery.md)
- [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
- [SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
- [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)  
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)

 

 

