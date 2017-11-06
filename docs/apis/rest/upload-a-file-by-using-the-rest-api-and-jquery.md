---
title: "Отправка файла с помощью REST API и jQuery"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 891b9682406188b0c5dff9f07161c1da8ca25739
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="upload-a-file-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="9e3cf-102">Отправка файла с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="9e3cf-102">Upload a file by using the REST API and jQuery</span></span>
<span data-ttu-id="9e3cf-103">Узнайте, как добавить локальный файл в папку SharePoint с помощью REST API и AJAX-запросов jQuery.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-103">Learn how to upload a local file to a SharePoint folder by using the REST API and jQuery AJAX requests.</span></span>
 
<span data-ttu-id="9e3cf-104">В примерах кода в этой статье показано, как с помощью интерфейса REST и AJAX-запросов jQuery добавить локальный файл в библиотеку **Документы**, а затем изменить свойства элемента списка, представляющего отправленный файл.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-104">The code examples in this article use the REST interface and jQuery AJAX requests to add a local file to the  **Documents** library and then change properties of the list item that represents the uploaded file.</span></span>
 
<span data-ttu-id="9e3cf-105">Выполните следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-105">This process uses the following high-level steps:</span></span>

1. <span data-ttu-id="9e3cf-p101">Преобразуйте локальный файл в буфер массива с помощью API **FileReader** (необходима поддержка HTML5). Функция **jQuery(document).ready** проверяет, поддерживает ли браузер API FileReader.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-p101">Convert the local file to an array buffer by using the  **FileReader** API, which requires HTML5 support. The **jQuery(document).ready** function checks for FileReader API support in the browser.</span></span>
    
2. <span data-ttu-id="9e3cf-p102">Добавьте файл в папку **Общие документы**, используя метод **Add** для коллекции файлов папки. Буфер массива передается в тексте запроса POST.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-p102">Add the file to the  **Shared Documents** folder by using the **Add** method on the folder's file collection. The array buffer is passed in the body of the POST request.</span></span>
    
    <span data-ttu-id="9e3cf-110">В этих примерах для получения коллекции используется конечная точка **getfolderbyserverrelativeurl**, но вы также можете использовать конечную точку списка (пример: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-110">These examples use the  **getfolderbyserverrelativeurl** endpoint to reach the file collection, but you can also use a list endpoint (example: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span></span>
    
3. <span data-ttu-id="9e3cf-111">Получите элемент списка, соответствующий отправленному файлу, используя свойство **ListItemAllFields** этого файла.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-111">Get the list item that corresponds to the uploaded file by using the  **ListItemAllFields** property of the uploaded file.</span></span>

4. <span data-ttu-id="9e3cf-112">Измените отображаемое имя и заголовок элемента списка с помощью запроса MERGE.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-112">Change the display name and title of the list item by using a MERGE request.</span></span>

## <a name="running-the-code-examples"></a><span data-ttu-id="9e3cf-113">Выполнение примеров кода</span><span class="sxs-lookup"><span data-stu-id="9e3cf-113">Running the code examples</span></span>
<span data-ttu-id="9e3cf-114"><a name="RunTheExamples"> </a> В обоих примерах кода в этой статье показано, как с помощью REST API и AJAX-запросов jQuery отправить файл в библиотеку **Общие документы**, а затем изменить свойства элемента списка.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-114"><a name="RunTheExamples"> </a> Both code examples in this article use the REST API and jQuery AJAX requests to upload a file to the  **Shared Documents** folder and then change list item properties.</span></span> <span data-ttu-id="9e3cf-115">В первом примере вызовы выполняются между доменами SharePoint с помощью метода **SP.AppContextSite**. Аналогичный код используется надстройкой, размещенной в SharePoint, при отправке файлов на хост-сайт.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-115">The first example uses **SP.AppContextSite** to make calls across SharePoint domains, like a SharePoint-hosted add-in would do when uploading files to the host web.</span></span> <span data-ttu-id="9e3cf-116">Во втором примере вызовы выполняются в пределах домена. Аналогичный код используется серверным решением и надстройкой, размещенной в SharePoint, и при отправке файлов на сайт.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-116">The second example makes same-domain calls, like a SharePoint-hosted add-in would do when uploading files to the add-in web, or a solution that's running on the server would do when uploading files.</span></span>

 <span data-ttu-id="9e3cf-p104">**Примечание.** Размещенные у поставщика надстройки, написанные на JavaScript, для отправки запросов в домен SharePoint должны использовать междоменную библиотеку SP.RequestExecutor. [Пример добавления файла с помощью междоменной библиотеки](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx#bk_FileCollectionAdd)</span><span class="sxs-lookup"><span data-stu-id="9e3cf-p104">**Note**  Provider-hosted add-ins written in JavaScript must use the SP.RequestExecutor cross-domain library to send requests to a SharePoint domain. For an example, see  [upload a file by using the cross-domain library](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx#bk_FileCollectionAdd).</span></span>
 
<span data-ttu-id="9e3cf-119">Чтобы воспользоваться примерами, описанными в этой статье, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-119">To use the examples in this article, you'll need the following:</span></span>
 
- <span data-ttu-id="9e3cf-120">SharePoint Server 2013, 2016 или SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-120">SharePoint Server 2013, 2016 or SharePoint Online</span></span>
-  <span data-ttu-id="9e3cf-p105">Разрешения на **запись** в библиотеку **Документы** для пользователя, который запускает код. Если вы разрабатываете надстройку SharePoint, то можете указать разрешения на **запись** на уровне **списка**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-p105">**Write** permissions to the **Documents** library for the user running the code. If you're developing a SharePoint Add-in, you can specify **Write** add-in permissions at the **List** scope</span></span>
- <span data-ttu-id="9e3cf-123">Поддержка API **FileReader** браузером (HTML5).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-123">Browser support for the  **FileReader** API (HTML5)</span></span>
- <span data-ttu-id="9e3cf-p106">Ссылка на библиотеку jQuery в разметке страницы. Пример:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-p106">A reference to the jQuery library in your page markup. For example:</span></span>
    
```
  <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js" type="text/javascript"></script>
```

- <span data-ttu-id="9e3cf-126">Следующие элементы управления в разметке страницы.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-126">The following controls in your page markup.</span></span>
    
```
  <input id="getFile" type="file"/><br />
  <input id="displayName" type="text" value="Enter a unique name" /><br />
  <input id="addFileButton" type="button" value="Upload" onclick="uploadFile()"/>
```


## <a name="code-example-1-upload-a-file-across-sharepoint-domains-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="9e3cf-127">Пример кода 1. Отправка файла между доменами SharePoint с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="9e3cf-127">Code example 1: Upload a file across SharePoint domains by using the REST API and jQuery</span></span>
<span data-ttu-id="9e3cf-128"><a name="RunTheExamples"> </a> В следующем примере кода показано, как с помощью REST API SharePoint и AJAX-запросов jQuery отправить файл в библиотеку **Документы** и изменить свойства элемента списка, представляющего этот файл.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-128">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the  **Documents** library and to change properties of the list item that represents the file. The context for this example is a SharePoint-hosted add-in that uploads a file to a folder on the host web.</span></span> <span data-ttu-id="9e3cf-129">Аналогичный код можно найти в размещенной в SharePoint надстройке, которая отправляет файлы в папку на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-129">The context for this example is a SharePoint-hosted add-in that uploads a file to a folder on the host web.</span></span>
 
<span data-ttu-id="9e3cf-130">Чтобы воспользоваться этим примером, ваша среда должна соответствовать [этим требованиям](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-130">You need to meet  [these requirements](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) to use this example.</span></span>
 
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


## <a name="code-example-2-upload-a-file-in-the-same-domain-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="9e3cf-131">Пример кода 2. Отправка файла в пределах домена с помощью REST API и jQuery</span><span class="sxs-lookup"><span data-stu-id="9e3cf-131">Code example 2: Upload a file in the same domain by using the REST API and jQuery</span></span>
<span data-ttu-id="9e3cf-132"><a name="UploadFile"> </a> В следующем примере кода показано, как с помощью REST API SharePoint и AJAX-запросов jQuery отправить файл в библиотеку **Документы** и изменить свойства элемента списка, представляющего этот файл.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-132">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the  **Documents** library and to change properties of the list item that represents the file. The context for this example is a SharePoint-hosted add-in that uploads a file to a folder on the host web.</span></span> <span data-ttu-id="9e3cf-133">Аналогичный код можно найти в серверном решении и</span><span class="sxs-lookup"><span data-stu-id="9e3cf-133">The context for this example is a solution that's running on the server.</span></span> <span data-ttu-id="9e3cf-134">размещенной в SharePoint надстройке, которая отправляет файлы на сайт.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-134">The code would be similar in a SharePoint-hosted add-in that uploads files to the add-in web.</span></span>
 
<span data-ttu-id="9e3cf-135">Чтобы воспользоваться этим примером, ваша среда должна соответствовать [этим требованиям](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-135">You need to meet  [these requirements](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) before you can run this example.</span></span>
 
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

## <a name="additional-resources"></a><span data-ttu-id="9e3cf-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9e3cf-136">Additional resources</span></span>
<span data-ttu-id="9e3cf-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9e3cf-137"></span></span>

-  [<span data-ttu-id="9e3cf-138">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9e3cf-138">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="9e3cf-139">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="9e3cf-139">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="9e3cf-140">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="9e3cf-140">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="9e3cf-141">Справочные материалы по интерфейсу API службы REST и примеры</span><span class="sxs-lookup"><span data-stu-id="9e3cf-141">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="9e3cf-142">Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="9e3cf-142">Access SharePoint data from add-ins using the cross-domain library</span></span>](../../sp-add-ins/access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)