---
title: Отправка файла с помощью API REST и jQuery
description: Отправка локального файла в папку SharePoint с помощью API REST и AJAX-запросов jQuery.
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 61a6b163f684ffd42135f3854ff10d46a029e841
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="upload-a-file-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="a69f0-103">Отправка файла с помощью API REST и jQuery</span><span class="sxs-lookup"><span data-stu-id="a69f0-103">Upload a file by using the REST API and jQuery</span></span>

<span data-ttu-id="a69f0-104">В примерах кода в этой статье показано, как с помощью интерфейса REST и AJAX-запросов jQuery добавить локальный файл в библиотеку **Documents** (Документы), а затем изменить свойства элемента списка, представляющего отправленный файл.</span><span class="sxs-lookup"><span data-stu-id="a69f0-104">The code examples in this article use the REST interface and jQuery AJAX requests to add a local file to the  **Documents** library and then change properties of the list item that represents the uploaded file.</span></span>

<span data-ttu-id="a69f0-105">Выполните следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="a69f0-105">This process uses the following high-level steps:</span></span>

1. <span data-ttu-id="a69f0-p101">Преобразование локального файла в буфер массива с помощью **FileReader** API, для чего необходима поддержка HTML5. Функция **jQuery(document).ready** проверяет поддержку FileReader API в браузере.</span><span class="sxs-lookup"><span data-stu-id="a69f0-p101">Convert the local file to an array buffer by using the **FileReader** API, which requires HTML5 support. The **jQuery(document).ready** function checks for FileReader API support in the browser.</span></span>
    
2. <span data-ttu-id="a69f0-p102">Добавление файла в папку **Общие документы** с помощью метода **Add** в коллекции файлов папки. Буфер массива передается в тексте запроса POST.</span><span class="sxs-lookup"><span data-stu-id="a69f0-p102">Add the file to the **Shared Documents** folder by using the **Add** method on the folder's file collection. The array buffer is passed in the body of the POST request.</span></span>
    
    <span data-ttu-id="a69f0-110">В этих примерах для доступа к коллекции файлов используется конечная точка **getfolderbyserverrelativeurl**, но также можно воспользоваться конечной точкой списка (например,  `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span><span class="sxs-lookup"><span data-stu-id="a69f0-110">These examples use the **getfolderbyserverrelativeurl** endpoint to reach the file collection, but you can also use a list endpoint (example: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span></span>
    
3. <span data-ttu-id="a69f0-111">Получение элемента списка, соответствующего загруженному файлу, с помощью свойства **ListItemAllFields** файла.</span><span class="sxs-lookup"><span data-stu-id="a69f0-111">Get the list item that corresponds to the uploaded file by using the **ListItemAllFields** property of the uploaded file.</span></span>
    
4. <span data-ttu-id="a69f0-112">Измените отображаемое имя и заголовок элемента списка с помощью запроса MERGE.</span><span class="sxs-lookup"><span data-stu-id="a69f0-112">Change the display name and title of the list item by using a MERGE request.</span></span>


<span data-ttu-id="a69f0-113"><a name="RunTheExamples"> </a></span><span class="sxs-lookup"><span data-stu-id="a69f0-113"></span></span>

## <a name="running-the-code-examples"></a><span data-ttu-id="a69f0-114">Выполнение примеров кода</span><span class="sxs-lookup"><span data-stu-id="a69f0-114">Running the code examples</span></span>

<span data-ttu-id="a69f0-115">В обоих примерах кода в этой статье показано, как с помощью API REST и AJAX-запросов jQuery отправить файл в библиотеку **Shared Documents** (Общие документы), а затем изменить свойства элемента списка.</span><span class="sxs-lookup"><span data-stu-id="a69f0-115"> Both code examples in this article use the REST API and jQuery AJAX requests to upload a file to the  **Shared Documents** folder and then change list item properties.</span></span> 

<span data-ttu-id="a69f0-116">В первом примере вызовы выполняются между доменами SharePoint с помощью метода **SP.AppContextSite**. Аналогичный код используется надстройкой, размещенной в SharePoint, при отправке файлов на хост-сайт.</span><span class="sxs-lookup"><span data-stu-id="a69f0-116">The first example uses **SP.AppContextSite** to make calls across SharePoint domains, like a SharePoint-hosted add-in would do when uploading files to the host web.</span></span> 

<span data-ttu-id="a69f0-117">Во втором примере вызовы выполняются в пределах домена. Аналогичный код используется серверным решением и надстройкой, размещенной в SharePoint, и при отправке файлов на сайт.</span><span class="sxs-lookup"><span data-stu-id="a69f0-117">The second example makes same-domain calls, like a SharePoint-hosted add-in would do when uploading files to the add-in web, or a solution that's running on the server would do when uploading files.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="a69f0-118">Размещаемые у поставщика надстройки, написанные на JavaScript, для отправки запросов в домен SharePoint должны использовать междоменную библиотеку SP.RequestExecutor.</span><span class="sxs-lookup"><span data-stu-id="a69f0-118">Provider-hosted add-ins written in JavaScript must use the SP.RequestExecutor cross-domain library to send requests to a SharePoint domain.</span></span> <span data-ttu-id="a69f0-119">См. пример [отправки файла с помощью междоменной библиотеки](https://msdn.microsoft.com/ru-RU/library/office/dn450841.aspx).</span><span class="sxs-lookup"><span data-stu-id="a69f0-119">For an example, see  [upload a file by using the cross-domain library](https://msdn.microsoft.com/ru-RU/library/office/dn450841.aspx).</span></span>
 
<span data-ttu-id="a69f0-120">Чтобы воспользоваться примерами, описанными в этой статье, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="a69f0-120">To use the examples in this article, you'll need the following:</span></span>

- <span data-ttu-id="a69f0-121">SharePoint Server или SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="a69f0-121">SharePoint Server or SharePoint Online</span></span>

- <span data-ttu-id="a69f0-122">Разрешения **Write** для библиотеки **Documents** (Документы) у пользователя, который запускает код.</span><span class="sxs-lookup"><span data-stu-id="a69f0-122">**Write** permissions to the **Documents** library for the user running the code. If you're developing a spappsing, you can specify Write add-in permissions at the List scope</span></span> <span data-ttu-id="a69f0-123">Если вы разрабатываете надстройку SharePoint, то можете указать для нее разрешения **Write** в области **List**.</span><span class="sxs-lookup"><span data-stu-id="a69f0-123">Write permissions to the Documents library for the user running the code. If you're developing a SharePoint Add-in, you can specify **Write** add-in permissions at the **List** scope</span></span>

- <span data-ttu-id="a69f0-124">Поддержка API **FileReader** браузером (HTML5).</span><span class="sxs-lookup"><span data-stu-id="a69f0-124">Browser support for the  **FileReader** API (HTML5)</span></span>

- <span data-ttu-id="a69f0-p105">Ссылка на библиотеку jQuery в разметке страницы. Пример:</span><span class="sxs-lookup"><span data-stu-id="a69f0-p105">A reference to the jQuery library in your page markup. For example:</span></span>
    
    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js" type="text/javascript"></script>
    ```
- <span data-ttu-id="a69f0-127">Приведенные ниже элементы управления в разметке страницы.</span><span class="sxs-lookup"><span data-stu-id="a69f0-127">The following controls in your page markup.</span></span>
    
    ```HTML
    <input id="getFile" type="file"/><br />
    <input id="displayName" type="text" value="Enter a unique name" /><br />
    <input id="addFileButton" type="button" value="Upload" onclick="uploadFile()"/>
    ```

<span data-ttu-id="a69f0-128"><a name="CodeExample1"> </a></span><span class="sxs-lookup"><span data-stu-id="a69f0-128"></span></span>

## <a name="code-example-1-upload-a-file-across-sharepoint-domains-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="a69f0-129">Пример кода 1. Отправка файла между доменами SharePoint с помощью API REST и jQuery</span><span class="sxs-lookup"><span data-stu-id="a69f0-129">Code example 1: Upload a file across SharePoint domains by using the REST API and jQuery</span></span>

<span data-ttu-id="a69f0-p106">Следующий пример кода использует API REST SharePoint и запросов jQuery AJAX для загрузки файла в библиотеку **Документы** и изменения свойств элемента списка, представляющего файл. Контекст этого примера размещенное в SharePoint надстройку, которая загружает файл в папку на хост-сервере.</span><span class="sxs-lookup"><span data-stu-id="a69f0-p106">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the **Documents** library and to change properties of the list item that represents the file. The context for this example is a SharePoint-hosted add-in that uploads a file to a folder on the host web.</span></span>

<span data-ttu-id="a69f0-132">Чтобы воспользоваться этим примером, ваша среда должна соответствовать [этим требованиям](#RunTheExamples).</span><span class="sxs-lookup"><span data-stu-id="a69f0-132">You need to meet  [these requirements](#RunTheExamples) to use this example.</span></span>
 

```javascript
'use strict';

var appWebUrl, hostWebUrl;

jQuery(document).ready(function () {

    // Check for FileReader API (HTML5) support.
    if (!window.FileReader) {
        alert('This browser does not support the FileReader API.');
    }

    // Get the add-in web and host web URLs.
    appWebUrl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
    hostWebUrl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
});

// Upload the file.
// You can upload files up to 2 GB with the REST API.
function uploadFile() {

    // Define the folder path for this example.
    var serverRelativeUrlToFolder = '/shared documents';

    // Get test values from the file input and text input page controls.
    // The display name must be unique every time you run the example.
    var fileInput = jQuery('#getFile');
    var newName = jQuery('#displayName').val();

    // Initiate method calls using jQuery promises.
    // Get the local file as an array buffer.
    var getFile = getFileBuffer();
    getFile.done(function (arrayBuffer) {

        // Add the file to the SharePoint folder.
        var addFile = addFileToFolder(arrayBuffer);
        addFile.done(function (file, status, xhr) {

            // Get the list item that corresponds to the uploaded file.
            var getItem = getListItem(file.d.ListItemAllFields.__deferred.uri);
            getItem.done(function (listItem, status, xhr) {

                // Change the display name and title of the list item.
                var changeItem = updateListItem(listItem.d.__metadata);
                changeItem.done(function (data, status, xhr) {
                    alert('file uploaded and updated');
                });
                changeItem.fail(onError);
            });
            getItem.fail(onError);
        });
        addFile.fail(onError);
    });
    getFile.fail(onError);

    // Get the local file as an array buffer.
    function getFileBuffer() {
        var deferred = jQuery.Deferred();
        var reader = new FileReader();
        reader.onloadend = function (e) {
            deferred.resolve(e.target.result);
        }
        reader.onerror = function (e) {
            deferred.reject(e.target.error);
        }
        reader.readAsArrayBuffer(fileInput[0].files[0]);
        return deferred.promise();
    }

    // Add the file to the file collection in the Shared Documents folder.
    function addFileToFolder(arrayBuffer) {

        // Get the file name from the file input control on the page.
        var parts = fileInput[0].value.split('\\');
        var fileName = parts[parts.length - 1];

        // Construct the endpoint.
        var fileCollectionEndpoint = String.format(
            "{0}/_api/sp.appcontextsite(@target)/web/getfolderbyserverrelativeurl('{1}')/files" +
            "/add(overwrite=true, url='{2}')?@target='{3}'",
            appWebUrl, serverRelativeUrlToFolder, fileName, hostWebUrl);

        // Send the request and return the response.
        // This call returns the SharePoint file.
        return jQuery.ajax({
            url: fileCollectionEndpoint,
            type: "POST",
            data: arrayBuffer,
            processData: false,
            headers: {
                "accept": "application/json;odata=verbose",
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-length": arrayBuffer.byteLength
            }
        });
    }

    // Get the list item that corresponds to the file by calling the file's ListItemAllFields property.
    function getListItem(fileListItemUri) {

        // Construct the endpoint.
        // The list item URI uses the host web, but the cross-domain call is sent to the
        // add-in web and specifies the host web as the context site.
        fileListItemUri = fileListItemUri.replace(hostWebUrl, '{0}');
        fileListItemUri = fileListItemUri.replace('_api/Web', '_api/sp.appcontextsite(@target)/web');
        
        var listItemAllFieldsEndpoint = String.format(fileListItemUri + "?@target='{1}'",
            appWebUrl, hostWebUrl);

        // Send the request and return the response.
        return jQuery.ajax({
            url: listItemAllFieldsEndpoint,
            type: "GET",
            headers: { "accept": "application/json;odata=verbose" }
        });
    }

    // Change the display name and title of the list item.
    function updateListItem(itemMetadata) {

        // Construct the endpoint.
        // Specify the host web as the context site.
        var listItemUri = itemMetadata.uri.replace('_api/Web', '_api/sp.appcontextsite(@target)/web');
        var listItemEndpoint = String.format(listItemUri + "?@target='{0}'", hostWebUrl);

        // Define the list item changes. Use the FileLeafRef property to change the display name. 
        // For simplicity, also use the name as the title.
        // The example gets the list item type from the item's metadata, but you can also get it from the
        // ListItemEntityTypeFullName property of the list.
        var body = String.format("{{'__metadata':{{'type':'{0}'}},'FileLeafRef':'{1}','Title':'{2}'}}",
            itemMetadata.type, newName, newName);

        // Send the request and return the promise.
        // This call does not return response content from the server.
        return jQuery.ajax({
            url: listItemEndpoint,
            type: "POST",
            data: body,
            headers: {
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-type": "application/json;odata=verbose",
                "content-length": body.length,
                "IF-MATCH": itemMetadata.etag,
                "X-HTTP-Method": "MERGE"
            }
        });
    }
}

// Display error messages. 
function onError(error) {
    alert(error.responseText);
}

// Get parameters from the query string.
// For production purposes you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var singleParam = params[i].split("=");
        if (singleParam[0] == paramToRetrieve) return singleParam[1];
    }
}
```

<br/>

<span data-ttu-id="a69f0-133"><a name="CodeExample2"> </a></span><span class="sxs-lookup"><span data-stu-id="a69f0-133"></span></span>

## <a name="code-example-2-upload-a-file-in-the-same-domain-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="a69f0-134">Пример кода 2. Отправка файла в пределах домена с помощью API REST и jQuery</span><span class="sxs-lookup"><span data-stu-id="a69f0-134">Code example 2: Upload a file in the same domain by using the REST API and jQuery</span></span>

<span data-ttu-id="a69f0-p107">Следующий пример кода использует API REST SharePoint и запросов jQuery AJAX для загрузки файла в библиотеку **Документы** и изменения свойств элемента списка, представляющего файл. Контекст этого примера решение, работающее на сервере. Код аналогичен коду надстройки с размещением в SharePoint, которое загружает файл на сайт надстройки.</span><span class="sxs-lookup"><span data-stu-id="a69f0-p107">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the **Documents** library and to change properties of the list item that represents the file. The context for this example is a solution that's running on the server. The code would be similar in a SharePoint-hosted add-in that uploads files to the add-in web.</span></span>

<span data-ttu-id="a69f0-138">Чтобы вы могли воспользоваться этим примером, нужно выполнить [эти требования](#RunTheExamples).</span><span class="sxs-lookup"><span data-stu-id="a69f0-138">You need to meet  [these requirements](#RunTheExamples) before you can run this example.</span></span> 

```javascript
'use strict';

jQuery(document).ready(function () {

    // Check for FileReader API (HTML5) support.
    if (!window.FileReader) {
        alert('This browser does not support the FileReader API.');
    }
});

// Upload the file.
// You can upload files up to 2 GB with the REST API.
function uploadFile() {

    // Define the folder path for this example.
    var serverRelativeUrlToFolder = '/shared documents';

    // Get test values from the file input and text input page controls.
    var fileInput = jQuery('#getFile');
    var newName = jQuery('#displayName').val();

    // Get the server URL.
    var serverUrl = _spPageContextInfo.webAbsoluteUrl;

    // Initiate method calls using jQuery promises.
    // Get the local file as an array buffer.
    var getFile = getFileBuffer();
    getFile.done(function (arrayBuffer) {

        // Add the file to the SharePoint folder.
        var addFile = addFileToFolder(arrayBuffer);
        addFile.done(function (file, status, xhr) {

            // Get the list item that corresponds to the uploaded file.
            var getItem = getListItem(file.d.ListItemAllFields.__deferred.uri);
            getItem.done(function (listItem, status, xhr) {

                // Change the display name and title of the list item.
                var changeItem = updateListItem(listItem.d.__metadata);
                changeItem.done(function (data, status, xhr) {
                    alert('file uploaded and updated');
                });
                changeItem.fail(onError);
            });
            getItem.fail(onError);
        });
        addFile.fail(onError);
    });
    getFile.fail(onError);

    // Get the local file as an array buffer.
    function getFileBuffer() {
        var deferred = jQuery.Deferred();
        var reader = new FileReader();
        reader.onloadend = function (e) {
            deferred.resolve(e.target.result);
        }
        reader.onerror = function (e) {
            deferred.reject(e.target.error);
        }
        reader.readAsArrayBuffer(fileInput[0].files[0]);
        return deferred.promise();
    }

    // Add the file to the file collection in the Shared Documents folder.
    function addFileToFolder(arrayBuffer) {

        // Get the file name from the file input control on the page.
        var parts = fileInput[0].value.split('\\');
        var fileName = parts[parts.length - 1];

        // Construct the endpoint.
        var fileCollectionEndpoint = String.format(
                "{0}/_api/web/getfolderbyserverrelativeurl('{1}')/files" +
                "/add(overwrite=true, url='{2}')",
                serverUrl, serverRelativeUrlToFolder, fileName);

        // Send the request and return the response.
        // This call returns the SharePoint file.
        return jQuery.ajax({
            url: fileCollectionEndpoint,
            type: "POST",
            data: arrayBuffer,
            processData: false,
            headers: {
                "accept": "application/json;odata=verbose",
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-length": arrayBuffer.byteLength
            }
        });
    }

    // Get the list item that corresponds to the file by calling the file's ListItemAllFields property.
    function getListItem(fileListItemUri) {

        // Send the request and return the response.
        return jQuery.ajax({
            url: fileListItemUri,
            type: "GET",
            headers: { "accept": "application/json;odata=verbose" }
        });
    }

    // Change the display name and title of the list item.
    function updateListItem(itemMetadata) {

        // Define the list item changes. Use the FileLeafRef property to change the display name. 
        // For simplicity, also use the name as the title. 
        // The example gets the list item type from the item's metadata, but you can also get it from the
        // ListItemEntityTypeFullName property of the list.
        var body = String.format("{{'__metadata':{{'type':'{0}'}},'FileLeafRef':'{1}','Title':'{2}'}}",
            itemMetadata.type, newName, newName);

        // Send the request and return the promise.
        // This call does not return response content from the server.
        return jQuery.ajax({
            url: itemMetadata.uri,
            type: "POST",
            data: body,
            headers: {
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-type": "application/json;odata=verbose",
                "content-length": body.length,
                "IF-MATCH": itemMetadata.etag,
                "X-HTTP-Method": "MERGE"
            }
        });
    }
}

// Display error messages. 
function onError(error) {
    alert(error.responseText);
}
```

<br/>

## <a name="see-also"></a><span data-ttu-id="a69f0-139">См. также</span><span class="sxs-lookup"><span data-stu-id="a69f0-139">See also</span></span>
<span data-ttu-id="a69f0-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a69f0-140"></span></span>

- [<span data-ttu-id="a69f0-141">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a69f0-141">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="a69f0-142">Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="a69f0-142">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)
- [<span data-ttu-id="a69f0-143">Справочные материалы и примеры по API REST</span><span class="sxs-lookup"><span data-stu-id="a69f0-143">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="a69f0-144">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="a69f0-144">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [<span data-ttu-id="a69f0-145">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="a69f0-145">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)

    
 

    
 

