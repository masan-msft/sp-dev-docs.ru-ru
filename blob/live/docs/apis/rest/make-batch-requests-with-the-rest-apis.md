---
title: "Отправка пакетных запросов с помощью интерфейсов REST API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b415b086175b366fbbc6d920186198b096cc85c7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="make-batch-requests-with-the-rest-apis"></a><span data-ttu-id="46647-102">Отправка пакетных запросов с помощью интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="46647-102">Make batch requests with the REST APIs</span></span>
<span data-ttu-id="46647-103">Узнайте, как использовать параметр запроса `$batch` с интерфейсами REST API и OData API.</span><span class="sxs-lookup"><span data-stu-id="46647-103">Learn how to use the  `$batch` query option with the REST/OData APIs.</span></span>
 
<span data-ttu-id="46647-p101">В этой статье описана отправка пакетных запросов и операций в случае REST API или OData API для Microsoft SharePoint Online (а также локальной среды SharePoint 2016 и более поздних версий), а также в случае [подмножества файлов и папок](http://msdn.microsoft.com/en-us/office/office365/api/files-rest-operations) REST API для Office 365. С помощью этой методики вы можете повысить производительность надстройки, совместив множество операций в одном запросе к серверу и одном отклике.</span><span class="sxs-lookup"><span data-stu-id="46647-p101">This article describes how you can batch queries and operations against the REST/OData API of Microsoft SharePoint Online (and on-premise SharePoint 2016 and later) and the  [Files and folders subset](http://msdn.microsoft.com/en-us/office/office365/api/files-rest-operations) of the Office 365 REST APIs. With this technique you can improve the performance of your add-in by combining many operations into a single request to the server and a single response back.</span></span>

## <a name="executive-summary-of-the-batch-option"></a><span data-ttu-id="46647-106">Аннотация к параметру $batch</span><span class="sxs-lookup"><span data-stu-id="46647-106">Executive summary of the $batch option</span></span>
<span data-ttu-id="46647-p102">В SharePoint Online (и локальной среде SharePoint 2016 и более поздних версий), а также API Office 365 реализован параметр запроса OData `$batch`, поэтому вы можете следовать указаниям по его использованию из [официальной документации](http://www.odata.org/documentation/odata-version-3-0/batch-processing). Кроме того, вы можете ознакомиться с этой темой в блоге Эндрю Коннела (Andrew Connell). Начните с записи [Часть 1. Пакетные запросы REST API в SharePoint](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests). Напомним о некоторых важных факторах:</span><span class="sxs-lookup"><span data-stu-id="46647-p102">SharePoint Online (and on-premise SharePoint 2016 and later) and the Office 365 APIs implement the OData  `$batch` query option, so you can rely on [the official documentation](http://www.odata.org/documentation/odata-version-3-0/batch-processing) for details about how to use it. (Another option is to see Andrew Connell's blog posts on the subject beginning at [Part 1 - SharePoint REST API Batching](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests).) The following is only a reminder of the major points:</span></span>
 
- <span data-ttu-id="46647-109">URL-адрес запроса состоит из корневого URL-адреса службы и параметра `$batch`. Пример: `https://fabrikam.sharepoint.com/_api/$batch` или `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span><span class="sxs-lookup"><span data-stu-id="46647-109">The request URL consists of the root service URL and the  `$batch` option; for example, `https://fabrikam.sharepoint.com/_api/$batch` or `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span></span>
    
- <span data-ttu-id="46647-110">Тело HTTP-запроса относится к типу MIME *multipart/mixed*.</span><span class="sxs-lookup"><span data-stu-id="46647-110">The HTTP request body is MIME type  *multipart/mixed*  .</span></span>
    
- <span data-ttu-id="46647-111">Текст запроса делится на части, отделенные друг от друга граничной строкой, которая указывается в заголовке запроса.</span><span class="sxs-lookup"><span data-stu-id="46647-111">The body of the request is divided into parts that are separated from each other by a boundary string that is specified in the header of the request.</span></span>
    
- <span data-ttu-id="46647-112">У каждой части этого тела запроса есть команда HTTP и URL-адрес REST, а также внутреннее тело, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="46647-112">Each part of the body has its own HTTP verb and REST URL, and its own internal body when applicable.</span></span>
    
- <span data-ttu-id="46647-p103">Такая часть может быть операцией чтения (либо вызовом функции) или объектом ChangeSet из одной или нескольких операций записи (либо вызовов функций). Объект ChangeSet относится к типу MIME *multipart/mixed* с дочерними частями, содержащими операции вставки, обновления или удаления.</span><span class="sxs-lookup"><span data-stu-id="46647-p103">A part can be a read operation (or function invocation), or a ChangeSet of one or more write operations (or function invocations). A ChangeSet is itself a MIME type  *multipart/mixed*  with subparts that contain insert, update, or delete operations.</span></span>
    
     <span data-ttu-id="46647-p104">**Важно!** В настоящее время интерфейсы API для SharePoint и Office 365 не поддерживают функции "все или ничего" объектов ChangeSet, содержащих несколько операций. В случае сбоя какой-либо из дочерних операций остальные операции выполняются без отката.</span><span class="sxs-lookup"><span data-stu-id="46647-p104">**Important**  At this time, SharePoint and Office 365 APIs do not support "all or nothing" functionality for ChangeSets that have more than one operation within them. If any of the child operations fails, the others still complete and are not rolled back.</span></span>

## <a name="code-samples"></a><span data-ttu-id="46647-117">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="46647-117">Code samples</span></span>
<span data-ttu-id="46647-118">Примеры кода, в котором используется параметр запроса `$batch` для интерфейсов REST API или OData API в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="46647-118">Samples of code that uses the  `$batch` query option against the SharePoint REST/OData APIs:</span></span> 

-  <span data-ttu-id="46647-119">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span><span class="sxs-lookup"><span data-stu-id="46647-119">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span></span>
-  <span data-ttu-id="46647-120">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span><span class="sxs-lookup"><span data-stu-id="46647-120">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span></span>
    

## <a name="example-requests-and-responses"></a><span data-ttu-id="46647-121">Примеры запросов и откликов</span><span class="sxs-lookup"><span data-stu-id="46647-121">Example requests and responses</span></span>
<span data-ttu-id="46647-122">Ниже приведен пример необработанного HTTP-запроса, который пакетно обрабатывает две операции GET, которые извлекают названия всех элементов в двух разных списках.</span><span class="sxs-lookup"><span data-stu-id="46647-122">The following is an example of a raw HTTP request that batches two GET operations that retrieve the titles of all the items in two different lists.</span></span>

```
POST https://fabrikam.sharepoint.com/_api/$batch HTTP/1.1
Authorization: Bearer <access token omitted>
Content-Type: multipart/mixed; boundary=batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Host: fabrikam.sharepoint.com
Content-Length: 527
Expect: 100-continue

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('Composed%20Looks')/items?$select=Title HTTP/1.1

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('User%20Information%20List')/items?$select=Title HTTP/1.1

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1--

```

<span data-ttu-id="46647-123">Ниже приведен пример текста необработанного HTTP-запроса, который пакетно обрабатывает операцию DELETE для списка и операцию GET для списка списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="46647-123">The following is an example of the body of a raw HTTP request that batches a DELETE of a list and a GET of the SharePoint list-of-lists.</span></span>
 
```
POST https://fabrikam.sharepoint.com/_api/$batch HTTP/1.1
Authorization: Bearer <access token omitted>
Content-Type: multipart/mixed; boundary=batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Host: fabrikam.sharepoint.com
Content-Length: 647
Expect: 100-continue

--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Content-Type: multipart/mixed; boundary=changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d

--changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d
Content-Type: application/http
Content-Transfer-Encoding: binary

DELETE https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('OldList') HTTP/1.1
If-Match: "1"

--changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d--
--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists HTTP/1.1

--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e--
```


## <a name="links-to-helpful-libraries"></a><span data-ttu-id="46647-124">Ссылки на полезные библиотеки</span><span class="sxs-lookup"><span data-stu-id="46647-124">Links to helpful libraries</span></span>
<span data-ttu-id="46647-p105">Существуют библиотеки OData, поддерживающие пакетные запросы OData для множества языков. Ниже представлены два примера. Более полный список см. на странице [Библиотеки OData](http://www.odata.org/libraries/).</span><span class="sxs-lookup"><span data-stu-id="46647-p105">There are OData libraries that support OData batching for many languages. Two examples are below. For a more complete list, see  [OData Libraries](http://www.odata.org/libraries/).</span></span>

-  <span data-ttu-id="46647-p106">[Библиотека OData .NET](http://msdn.microsoft.com/en-us/office/microsoft.data.odata%28v=vs.90%29). Обратите особое внимание на классы **ODataBatch***.</span><span class="sxs-lookup"><span data-stu-id="46647-p106">[.NET OData library](http://msdn.microsoft.com/en-us/office/microsoft.data.odata%28v=vs.90%29). See especially the  **ODataBatch*** classes.</span></span>
-  <span data-ttu-id="46647-p107">[Библиотека Data.js](http://datajs.codeplex.com/documentation). Обратите особое внимание на [пакетные операции](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span><span class="sxs-lookup"><span data-stu-id="46647-p107">[Datajs library](http://datajs.codeplex.com/documentation). See especially  [Batch operations](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span></span>