---
title: "Отправка пакетных запросов с помощью REST API"
description: "Использование параметра запроса $batch с REST API или OData API."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 2d47912c995614c4ee9e12d6fef7f738287bceb1
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="make-batch-requests-with-the-rest-apis"></a><span data-ttu-id="47f6e-103">Отправка пакетных запросов с использованием REST API</span><span class="sxs-lookup"><span data-stu-id="47f6e-103">Make batch requests with the REST APIs</span></span>

<span data-ttu-id="47f6e-104">В этой статье описано выполнение пакетных запросов и операций при использовании REST API или OData API для Microsoft SharePoint Online (и локальной среды SharePoint 2016 и более поздних версий), а также при использовании [подмножества файлов и папок](https://msdn.microsoft.com/library) REST API для Office 365.</span><span class="sxs-lookup"><span data-stu-id="47f6e-104">This article describes how you can batch queries and operations against the REST/OData API of Microsoft SharePoint Online (and on-premise SharePoint 2016 and later) and the  [Files and folders subset](https://msdn.microsoft.com/library) of the Office 365 REST APIs. With this technique you can improve the performance of your add-in by combining many operations into a single request to the server and a single response back.</span></span> <span data-ttu-id="47f6e-105">С помощью этой методики вы можете повысить производительность надстройки, совместив множество операций в одном запросе к серверу и одном отклике.</span><span class="sxs-lookup"><span data-stu-id="47f6e-105">This article describes how you can batch queries and operations against the REST/OData API of Microsoft SharePoint Online (and on-premise SharePoint 2016 and later) and the  Files and folders subset of the Office 365 REST APIs. With this technique you can improve the performance of your add-in by combining many operations into a single request to the server and a single response back.</span></span>
 

## <a name="executive-summary-of-the-batch-option"></a><span data-ttu-id="47f6e-106">Краткий обзор параметра $batch</span><span class="sxs-lookup"><span data-stu-id="47f6e-106">Executive summary of the $batch option</span></span>

<span data-ttu-id="47f6e-107">В SharePoint Online (и локальной среде SharePoint 2016 и более поздних версий), а также API Office 365 реализован параметр запроса OData `$batch`, поэтому вы можете следовать указаниям по его использованию из [официальной документации](http://www.odata.org/documentation/odata-version-3-0/batch-processing).</span><span class="sxs-lookup"><span data-stu-id="47f6e-107">SharePoint Online (and on-premise SharePoint 2016 and later) and the Office 365 APIs implement the OData  `$batch` query option, so you can rely on [the official documentation](http://www.odata.org/documentation/odata-version-3-0/batch-processing) for details about how to use it. (Another option is to see Andrew Connell's blog posts on the subject beginning at Part 1 - SharePoint REST API Batching.) The following is only a reminder of the major points:</span></span> <span data-ttu-id="47f6e-108">Кроме того, вы можете ознакомиться с этой темой в блоге Andrew Connell. Начните с записи [Часть 1. Пакетные запросы REST API в SharePoint](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests).</span><span class="sxs-lookup"><span data-stu-id="47f6e-108">(Another option is to see Andrew Connell's blog posts on the subject beginning at [Part 1 - SharePoint REST API Batching](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests).)</span></span> 

<span data-ttu-id="47f6e-109">Напомним о некоторых важных факторах:</span><span class="sxs-lookup"><span data-stu-id="47f6e-109">The following is a reminder of the major points:</span></span>

- <span data-ttu-id="47f6e-110">URL-адрес запроса состоит из корневого URL-адреса службы и параметра `$batch`. Пример: `https://fabrikam.sharepoint.com/_api/$batch` или `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span><span class="sxs-lookup"><span data-stu-id="47f6e-110">The request URL consists of the root service URL and the  `$batch` option; for example, `https://fabrikam.sharepoint.com/_api/$batch` or `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span></span>

- <span data-ttu-id="47f6e-111">Тело HTTP-запроса относится к типу MIME *multipart/mixed*.</span><span class="sxs-lookup"><span data-stu-id="47f6e-111">The HTTP request body is MIME type *multipart/mixed*.</span></span>

- <span data-ttu-id="47f6e-112">Текст запроса делится на части, отделенные друг от друга граничной строкой, которая указывается в заголовке запроса.</span><span class="sxs-lookup"><span data-stu-id="47f6e-112">The body of the request is divided into parts that are separated from each other by a boundary string that is specified in the header of the request.</span></span>

- <span data-ttu-id="47f6e-113">У каждой части этого тела запроса есть команда HTTP и URL-адрес REST, а также внутреннее тело, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="47f6e-113">Each part of the body has its own HTTP verb and REST URL, and its own internal body when applicable.</span></span>

- <span data-ttu-id="47f6e-114">Такая часть может представлять собой операцию чтения (либо вызов функции) или объект ChangeSet из одной или нескольких операций записи (либо вызовов функций).</span><span class="sxs-lookup"><span data-stu-id="47f6e-114">A part can be a read operation (or function invocation), or a ChangeSet of one or more write operations (or function invocations). A ChangeSet is itself a MIME type  multipart/mixed  with subparts that contain insert, update, or delete operations.</span></span> <span data-ttu-id="47f6e-115">Объект ChangeSet относится к типу MIME *multipart/mixed* с дочерними частями, содержащими операции вставки, обновления или удаления.</span><span class="sxs-lookup"><span data-stu-id="47f6e-115">A part can be a read operation (or function invocation), or a ChangeSet of one or more write operations (or function invocations). A ChangeSet is itself a MIME type  *multipart/mixed*  with subparts that contain insert, update, or delete operations.</span></span>
    
> [!IMPORTANT] 
> <span data-ttu-id="47f6e-116">В настоящее время интерфейсы API для SharePoint и Office 365 не поддерживают функции "все или ничего" объектов ChangeSet, содержащих несколько операций.</span><span class="sxs-lookup"><span data-stu-id="47f6e-116">Important  At this time, SharePoint and Office 365 APIs do not support "all or nothing" functionality for ChangeSets that have more than one operation within them. If any of the child operations fails, the others still complete and are not rolled back.</span></span> <span data-ttu-id="47f6e-117">В случае сбоя какой-либо из дочерних операций остальные операции выполняются без отката.</span><span class="sxs-lookup"><span data-stu-id="47f6e-117">If any of the child operations fails, the others still complete and are not rolled back.</span></span>

## <a name="code-samples"></a><span data-ttu-id="47f6e-118">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="47f6e-118">Code samples</span></span>

<span data-ttu-id="47f6e-119">Примеры кода, в котором используется параметр запроса `$batch` для интерфейсов REST API или OData API SharePoint:</span><span class="sxs-lookup"><span data-stu-id="47f6e-119">Samples of code that uses the  `$batch` query option against the SharePoint REST/OData APIs:</span></span>

- <span data-ttu-id="47f6e-120">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span><span class="sxs-lookup"><span data-stu-id="47f6e-120">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span></span>

- <span data-ttu-id="47f6e-121">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span><span class="sxs-lookup"><span data-stu-id="47f6e-121">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span></span>
   
## <a name="example-requests-and-responses"></a><span data-ttu-id="47f6e-122">Примеры запросов и откликов</span><span class="sxs-lookup"><span data-stu-id="47f6e-122">Example requests and responses</span></span>

<span data-ttu-id="47f6e-123">Ниже приведен пример необработанного HTTP-запроса, который пакетно обрабатывает две операции GET, которые извлекают названия всех элементов в двух разных списках.</span><span class="sxs-lookup"><span data-stu-id="47f6e-123">The following is an example of a raw HTTP request that batches two GET operations that retrieve the titles of all the items in two different lists.</span></span>

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

<br/>

<span data-ttu-id="47f6e-124">Ниже приведен пример текста необработанного HTTP-запроса, который пакетно обрабатывает операцию DELETE для списка и операцию GET для списка списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="47f6e-124">The following is an example of the body of a raw HTTP request that batches a DELETE of a list and a GET of the SharePoint list-of-lists.</span></span>

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

<br/>

## <a name="odata-libraries"></a><span data-ttu-id="47f6e-125">Библиотеки OData</span><span class="sxs-lookup"><span data-stu-id="47f6e-125">OData libraries</span></span>

<span data-ttu-id="47f6e-126">Библиотеки OData, поддерживающие пакетные запросы OData для множества языков.</span><span class="sxs-lookup"><span data-stu-id="47f6e-126">OData libraries support OData batching for many languages.</span></span> <span data-ttu-id="47f6e-127">Ниже приведены два примера.</span><span class="sxs-lookup"><span data-stu-id="47f6e-127">Following are two examples.</span></span> <span data-ttu-id="47f6e-128">Более полный список см. на странице [Библиотеки OData](http://www.odata.org/libraries/).</span><span class="sxs-lookup"><span data-stu-id="47f6e-128">For a more complete list, see [OData Libraries](http://www.odata.org/libraries/).</span></span>

- <span data-ttu-id="47f6e-p106">[Библиотека OData .NET](http://msdn.microsoft.com/ru-RU/office/microsoft.data.odata%28v=vs.90%29). Обратите особое внимание на классы \*\*ODataBatch\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="47f6e-p106">[.NET OData library](http://msdn.microsoft.com/ru-RU/office/microsoft.data.odata%28v=vs.90%29). See especially the **ODataBatch**\* classes.</span></span>
- <span data-ttu-id="47f6e-131">[Библиотека datajs](http://datajs.codeplex.com/documentation).</span><span class="sxs-lookup"><span data-stu-id="47f6e-131">[Datajs library](http://datajs.codeplex.com/documentation).</span></span> <span data-ttu-id="47f6e-132">Обратите особое внимание на [пакетные операции](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span><span class="sxs-lookup"><span data-stu-id="47f6e-132">Datajs library. See especially  [Batch operations](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span></span>

## <a name="see-also"></a><span data-ttu-id="47f6e-133">См. также</span><span class="sxs-lookup"><span data-stu-id="47f6e-133">See also</span></span>

- [<span data-ttu-id="47f6e-134">Знакомство со службой REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="47f6e-134">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="47f6e-135">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="47f6e-135">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)

 

