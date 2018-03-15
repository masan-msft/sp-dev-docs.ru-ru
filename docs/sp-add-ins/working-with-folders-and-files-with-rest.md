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
# <a name="working-with-folders-and-files-with-rest"></a><span data-ttu-id="9661f-103">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="9661f-103">Working with folders and files with REST</span></span>

> [!TIP] 
> <span data-ttu-id="9661f-p101">Служба REST SharePoint Online (а также локальной среды SharePoint 2016 и более поздних версий) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData `$batch`. Дополнительные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="9661f-p101">`$batch`  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  [](make-batch-requests-with-the-rest-apis.md) query option. For details and links to code samples, see Make batch requests with the REST APIs.</span></span> 

<span data-ttu-id="9661f-106"><a name="Folders"> </a></span><span class="sxs-lookup"><span data-stu-id="9661f-106"></span></span>

## <a name="working-with-folders-by-using-rest"></a><span data-ttu-id="9661f-107">Работа с папками при помощи REST</span><span class="sxs-lookup"><span data-stu-id="9661f-107">Working with folders by using REST</span></span>

<span data-ttu-id="9661f-p102">Вы можете получить папку внутри библиотеки документов, если вы знаете ее URL-адрес. Например, вы можете получить корневую папку библиотеки совместно используемых документов с помощью конечной точки, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="9661f-p102">You can retrieve a folder inside a document library when you know its URL. For example, you can retrieve the root folder of your Shared Documents library by using the endpoint in the following example.</span></span>


```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="9661f-110">Ниже показан пример свойств папки, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="9661f-110">The following XML shows an example of folder properties that are returned when you request the XML content type.</span></span>

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

<span data-ttu-id="9661f-111">В следующем примере показано, как **создать** папку.</span><span class="sxs-lookup"><span data-stu-id="9661f-111">The following example shows how to **create** a folder.</span></span>

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

<span data-ttu-id="9661f-112">В следующем примере показано, как **обновить** папку, используя метод **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="9661f-112">The following example shows how to **update** a folder by using the **MERGE** method.</span></span>

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

<span data-ttu-id="9661f-113">В приведенном ниже примере показано, как **удалить** папку.</span><span class="sxs-lookup"><span data-stu-id="9661f-113">The following example shows how to **delete** a folder.</span></span>

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

<span data-ttu-id="9661f-114"><a name="Files"> </a></span><span class="sxs-lookup"><span data-stu-id="9661f-114"></span></span>

## <a name="working-with-files-by-using-rest"></a><span data-ttu-id="9661f-115">Работа с файлами при помощи REST</span><span class="sxs-lookup"><span data-stu-id="9661f-115">Working with files by using REST</span></span>

<span data-ttu-id="9661f-116">В приведенном ниже примере показано, как **получить** все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="9661f-116">The following example shows how to **retrieve** all of the files in a folder.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="9661f-117">В следующем примере показано, как **получить** конкретный файл.</span><span class="sxs-lookup"><span data-stu-id="9661f-117">The following example shows how to **retrieve** a specific file.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<br/>

<span data-ttu-id="9661f-118">Вы также можете **получить** файл, если вы знаете его URL-адрес, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="9661f-118">You can also **retrieve** a file when you know its URL, as in the following example.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<br/>

<span data-ttu-id="9661f-119">В следующем примере показано, как **создать** файл и добавить его в папку.</span><span class="sxs-lookup"><span data-stu-id="9661f-119">The following example shows how to **create** a file and add it to a folder.</span></span>

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

<span data-ttu-id="9661f-120">В следующем примере показано, как **обновить** файл, используя метод **PUT**.</span><span class="sxs-lookup"><span data-stu-id="9661f-120">The following example shows how to **update** a file by using the **PUT** method.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="9661f-121">Обновлять файлы можно только с помощью метода **PUT**.</span><span class="sxs-lookup"><span data-stu-id="9661f-121">**PUT** is the only method that you can use to update a file.</span></span> <span data-ttu-id="9661f-122">Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="9661f-122">The **MERGE** method is not allowed.</span></span>

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

<span data-ttu-id="9661f-123">Если вы хотите обновить метаданные файла, необходимо создать конечную точку, которая получает файл как элемент списка.</span><span class="sxs-lookup"><span data-stu-id="9661f-123">If you want to update a file's metadata, you have to construct an endpoint that reaches the file as a list item.</span></span> <span data-ttu-id="9661f-124">Это возможно, так как каждая папка также является списком, а каждый файл — элементом списка.</span><span class="sxs-lookup"><span data-stu-id="9661f-124">You can do this because each folder is also a list, and each file is also a list item.</span></span> <span data-ttu-id="9661f-125">Создайте такую конечную точку: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.</span><span class="sxs-lookup"><span data-stu-id="9661f-125">Construct an endpoint that looks like this: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.</span></span> <span data-ttu-id="9661f-126">Информацию о том, как обновить метаданные элемента списка, см. в статье [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9661f-126">For information about how to update a list item's metadata, see [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md).</span></span> 

<span data-ttu-id="9661f-127">Извлеките файл, чтобы никто не смог его изменить, прежде чем вы обновите его.</span><span class="sxs-lookup"><span data-stu-id="9661f-127">You may want to check out a file to make sure that no one changes it before you update it.</span></span> <span data-ttu-id="9661f-128">После обновления файл необходимо вернуть, чтобы другие пользователи могли с ним работать.</span><span class="sxs-lookup"><span data-stu-id="9661f-128">After your update, you should check the file back in so that others can work with it.</span></span> <span data-ttu-id="9661f-129">В приведенном ниже примере показано, как **извлечь файл**.</span><span class="sxs-lookup"><span data-stu-id="9661f-129">The following example shows you how to  **check a file in**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<br/>

<span data-ttu-id="9661f-130">В приведенном ниже примере показано, как **вернуть файл**.</span><span class="sxs-lookup"><span data-stu-id="9661f-130">The following example shows you how to **check a file in**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<br/>

<span data-ttu-id="9661f-131">В приведенном ниже примере показано, как **удалить** файл.</span><span class="sxs-lookup"><span data-stu-id="9661f-131">The following example shows how to **delete** a file.</span></span>

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

<span data-ttu-id="9661f-132"><a name="LargeFiles"> </a></span><span class="sxs-lookup"><span data-stu-id="9661f-132"></span></span>

## <a name="working-with-large-files-by-using-rest"></a><span data-ttu-id="9661f-133">Работа с большими файлами при помощи REST</span><span class="sxs-lookup"><span data-stu-id="9661f-133">Working with large files by using REST</span></span>

<span data-ttu-id="9661f-134">Отправить двоичный файл размером более 1,5 МБ можно только с помощью интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="9661f-134">When you need to upload a binary file that is larger than 1.5 megabytes (MB), the REST interface is your only option.</span></span> <span data-ttu-id="9661f-135">Пример кода для отправки двоичного файла размером менее 1,5 МБ с помощью объектной модели JavaScript SharePoint см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="9661f-135">See  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md) for a code example that shows you how to upload a binary file that is smaller than 1.5 MB by using the SharePoint Javascript object model.</span></span> <span data-ttu-id="9661f-136">Максимальный размер двоичного файла, который можно создать с помощью REST, составляет 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="9661f-136">The maximum size of a binary file that you can create with REST is 2 gigabytes (GB.md).</span></span> <span data-ttu-id="9661f-137">В приведенном ниже примере показано, как **создать** большой двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="9661f-137">The following example shows how to **create** a large binary file.</span></span>
 
> [!WARNING] 
> <span data-ttu-id="9661f-138">Этот способ работает только в Internet Explorer 10 и последних версиях других браузеров.</span><span class="sxs-lookup"><span data-stu-id="9661f-138">This approach will work only with Internet Explorer 10 and the latest versions of other browsers.</span></span>

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

<span data-ttu-id="9661f-139">В приведенном ниже примере кода показано, как создать файл с помощью этой конечной точки REST и междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="9661f-139">The following code sample shows how to create a file by using this REST endpoint and the cross-domain library.</span></span>

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

<span data-ttu-id="9661f-140"><a name="FileAttachments"> </a></span><span class="sxs-lookup"><span data-stu-id="9661f-140"></span></span>

## <a name="working-with-files-attached-to-list-items-by-using-rest"></a><span data-ttu-id="9661f-141">Работа со вложенными в элементы списка файлами при помощи REST</span><span class="sxs-lookup"><span data-stu-id="9661f-141">Working with files attached to list items by using REST</span></span>


<span data-ttu-id="9661f-142">В приведенном ниже примере показано, как **получить** все файлы, вложенные в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="9661f-142">The following example shows how to **retrieve** all of the files that are attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="9661f-143">В следующем примере показано, как **извлечь** файл, подключенный к элементу списка.</span><span class="sxs-lookup"><span data-stu-id="9661f-143">The following example shows how to **retrieve** a file that is attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="9661f-144">В следующем примере показано, как **создать** подключение файла к элементу списка.</span><span class="sxs-lookup"><span data-stu-id="9661f-144">The following example shows how to **create** a file attachment to a list item.</span></span>

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

<span data-ttu-id="9661f-145">В приведенном ниже примере показано, как **заменить** вложенный файл на элемент списка с помощью метода **PUT**.</span><span class="sxs-lookup"><span data-stu-id="9661f-145">The following example shows how to **update** a file attachment to a list item by using the **PUT** method.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="9661f-146">Обновлять файлы можно только с помощью метода **PUT**.</span><span class="sxs-lookup"><span data-stu-id="9661f-146">**PUT** is the only method that you can use to update a file.</span></span> <span data-ttu-id="9661f-147">Использовать метод **MERGE** запрещено.</span><span class="sxs-lookup"><span data-stu-id="9661f-147">The **MERGE** method is not allowed.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9661f-148">См. также</span><span class="sxs-lookup"><span data-stu-id="9661f-148">See also</span></span>
<span data-ttu-id="9661f-149"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9661f-149"></span></span>

- [<span data-ttu-id="9661f-150">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9661f-150">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="9661f-151">Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9661f-151">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)   
- [<span data-ttu-id="9661f-152">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="9661f-152">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="9661f-153">Отправка файла с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="9661f-153">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery.md)
- [<span data-ttu-id="9661f-154">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="9661f-154">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
- [<span data-ttu-id="9661f-155">SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST</span><span class="sxs-lookup"><span data-stu-id="9661f-155">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
- [<span data-ttu-id="9661f-156">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9661f-156">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [<span data-ttu-id="9661f-157">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9661f-157">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
- [<span data-ttu-id="9661f-158">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="9661f-158">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)  
- [<span data-ttu-id="9661f-159">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9661f-159">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)

 

 

