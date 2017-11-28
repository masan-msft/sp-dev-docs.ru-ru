---
title: "Поставщик идентификатора документа в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a20320887a17b26a4eb247b6c2968b82ab5d715b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="document-id-provider-in-the-sharepoint-add-in-model"></a><span data-ttu-id="84e59-102">Поставщик идентификатора документа в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="84e59-102">Document ID provider in the SharePoint add-in model</span></span>
===================================================

<a name="summary"></a><span data-ttu-id="84e59-103">Summary</span><span class="sxs-lookup"><span data-stu-id="84e59-103">Summary</span></span>
-------

<span data-ttu-id="84e59-104">Выбор подхода Присвоение уникальных идентификаторов для документов в SharePoint отличается новой модели надстройки SharePoint от был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="84e59-104">The approach you take to set unique identifiers for documents in SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="84e59-105">В типичных полного доверия кода (FTC) / сценарий решения фермы обработчиков событий элемента списка выполнение объектной модели SharePoint серверного кода были используется для задания уникальных идентификаторов для документов, и они были развернуты с помощью решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list item event handlers running SharePoint Server-side Object Model code were used to set unique identifiers for documents and they were deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="84e59-106">В модели сценарий надстройки SharePoint объектную модель SharePoint на стороне клиента (CSOM) и/или интерфейса API REST SharePoint используется для задания уникальных идентификаторов для документов.</span><span class="sxs-lookup"><span data-stu-id="84e59-106">In an SharePoint Add-in model scenario, the SharePoint Client-side Object Model (CSOM) and/or the SharePoint REST API are used to set unique identifiers for documents.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="84e59-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="84e59-107">High-level guidelines</span></span>
---------------------

<span data-ttu-id="84e59-108">Как правило эскиз мы хотели бы предоставляют следующие рекомендации высокого уровня для параметра уникальные идентификаторы документов в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-108">As a rule of a thumb, we would like to provide the following high-level guidelines for setting unique identifiers for documents in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="84e59-109">Использование SharePoint клиента со стороны объектной модели (CSOM) и/или API-интерфейсы REST SharePoint для указания уникальные идентификаторы документов.</span><span class="sxs-lookup"><span data-stu-id="84e59-109">Use the SharePoint Client Side Object Model (CSOM), and/or the SharePoint REST APIs to set unique identifiers for documents.</span></span>
- <span data-ttu-id="84e59-110">На данный момент нет не поддерживаемый механизм ожидания введите для сопоставления удаленных обработанные кода для замены поставщик идентификатора документа ожидания введите, поэтому эту возможность, не поддерживается изначально можно изменить с помощью API удаленного.</span><span class="sxs-lookup"><span data-stu-id="84e59-110">Currently, there is no supported out-of-the-box mechanism for associating remote processed code to replace the out-of-the-box document ID provider, so this capability is not natively supported to be modified with remote APIs.</span></span>
- <span data-ttu-id="84e59-111">Тем не менее как и во многих случаях с моделью надстройка альтернативные маршруты обсуждаемые.</span><span class="sxs-lookup"><span data-stu-id="84e59-111">However, like in many cases with the Add-in model, alternative routes are being explored.</span></span>

<a name="how-are-unique-identifiers-set-on-documents"></a><span data-ttu-id="84e59-112">Установке уникальных идентификаторов документов</span><span class="sxs-lookup"><span data-stu-id="84e59-112">How are unique identifiers set on documents?</span></span>
--------------------------------------------

<span data-ttu-id="84e59-113">***По сути настройка уникального идентификатора для документа означает, что установка значения столбца в библиотеке SharePoint списка или документов.***</span><span class="sxs-lookup"><span data-stu-id="84e59-113">***Essentially, setting a unique identifier for a document means setting the value of a column in a SharePoint list/document library.***</span></span>  

<span data-ttu-id="84e59-114">SharePoint (CSOM) и/или API-интерфейсы REST могут быть использованы для установки значений столбца и therefor они могут использоваться для задания уникальные идентификаторы документов.</span><span class="sxs-lookup"><span data-stu-id="84e59-114">The SharePoint (CSOM) and/or REST APIs may be used to set column values, and therefor they may be used to set unique identifiers for documents.</span></span> <span data-ttu-id="84e59-115">Обратитесь к следующим документам, чтобы узнать больше о эти интерфейсы API и как задать значения столбцов с ними.</span><span class="sxs-lookup"><span data-stu-id="84e59-115">See the following articles to learn more about these APIs and how to set column values with them.</span></span>  

- [<span data-ttu-id="84e59-116">Выполнения базовых операций с помощью кода клиента библиотеки SharePoint 2013 (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="84e59-116">Complete basic operations using SharePoint 2013 client library code (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx#BasicOps_SPListItemTasks) 
- [<span data-ttu-id="84e59-117">Работа со списками и элементами списка с помощью REST (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="84e59-117">Working with lists and list items with REST (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/dn292552.aspx#ListItems)

<a name="options-to-set-unique-identifiers-for-documents"></a><span data-ttu-id="84e59-118">Параметры, чтобы установить уникальных идентификаторов документов</span><span class="sxs-lookup"><span data-stu-id="84e59-118">Options to set unique identifiers for documents</span></span>
-----------------------------------------------
<span data-ttu-id="84e59-119">У вас есть несколько параметров для установки уникальных идентификаторов для документов, сохраняемых в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-119">You have a few options to set unique identifiers for documents stored in SharePoint.</span></span>

- <span data-ttu-id="84e59-120">Использование удаленных приемников событий</span><span class="sxs-lookup"><span data-stu-id="84e59-120">Use remote event receivers</span></span>
- <span data-ttu-id="84e59-121">Используйте в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="84e59-121">Use a background process</span></span>

<a name="use-remote-event-receivers"></a><span data-ttu-id="84e59-122">Использование удаленных приемников событий</span><span class="sxs-lookup"><span data-stu-id="84e59-122">Use remote event receivers</span></span>
--------------------------
<span data-ttu-id="84e59-123">В этом шаблоне удаленных приемников событий выполнялось в том случае, когда новые документы можно было выгрузить в библиотеках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-123">In this pattern, remote event receivers fire when new documents are uploaded to SharePoint libraries.</span></span> <span data-ttu-id="84e59-124">Приемники удаленных событий убедитесь, CSOM или интерфейса API REST вызывает Присвоение уникальных идентификаторов для документов.</span><span class="sxs-lookup"><span data-stu-id="84e59-124">The remote event receivers make CSOM or REST API calls to set unique identifiers for documents.</span></span>

- <span data-ttu-id="84e59-125">Этот шаблон выполняется сразу же после отправить документ в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-125">This pattern executes immediately after a document is uploaded to SharePoint.</span></span>
    + <span data-ttu-id="84e59-126">До тех пор, пока своевременного выполнения кода в службу, связанную с удаленного приемника событий, идентификаторы документов зависят от выбора быстро после загрузки документа в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-126">As long as the code in the service associated with the remote event receiver executes in a timely fashion, the document IDs are set quickly after a new document is uploaded to SharePoint.</span></span>
- <span data-ttu-id="84e59-127">Этот шаблон работает только на новые документы, отправленные в SharePoint, не выполнен уникальных идентификаторов для документов, уже хранятся в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-127">This pattern only operates on new documents uploaded to SharePoint, it does not set unique identifiers for documents already stored in SharePoint.</span></span>
- <span data-ttu-id="84e59-128">Массовые операции отправки, будет вызвано несколько вызовов службы, связанной с приемника удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="84e59-128">Bulk upload operations will trigger multiple calls to the service associated with the remote event receiver.</span></span> <span data-ttu-id="84e59-129">Составьте соответствующий план для обеспечения массовые операции отправки не будет перегрузить службу.</span><span class="sxs-lookup"><span data-stu-id="84e59-129">Plan accordingly to ensure bulk upload operations will not overload the service.</span></span>
- <span data-ttu-id="84e59-130">Нет возможности для удаленного приемника событий для уведомления SharePoint, если параметру идентификатор уникальный документа не удалось.</span><span class="sxs-lookup"><span data-stu-id="84e59-130">There is no way for a remote event receiver to notify SharePoint if setting a unique document ID failed.</span></span>

<span data-ttu-id="84e59-131">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="84e59-131">**When is it a good fit?**</span></span>

<span data-ttu-id="84e59-132">Если вам нужно быстро задать уникальные идентификаторы документов после их передачи в SharePoint и предполагается, что массовые операции отправки.</span><span class="sxs-lookup"><span data-stu-id="84e59-132">When you need to set unique identifiers for documents quickly after they are uploaded to SharePoint and you do not expect bulk upload operations.</span></span>

<span data-ttu-id="84e59-133">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="84e59-133">**Getting started**</span></span>

<span data-ttu-id="84e59-134">[Приемники событий и приемников событий List (добавить в SharePoint набора команд)](event-receiver-and-list-event-receiver-sharepoint-add-in.md) описывается, как реализовать приемников событий в модели надстройки и предоставляет ссылки на другие статьи и примеры.</span><span class="sxs-lookup"><span data-stu-id="84e59-134">The [Event Receivers and List Event Receivers (SharePoint Add-in Recipe)](event-receiver-and-list-event-receiver-sharepoint-add-in.md) describes how to implement event receivers in the Add-in model and provides links to several samples and articles.</span></span>

<a name="use-a-background-process"></a><span data-ttu-id="84e59-135">Используйте в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="84e59-135">Use a background process</span></span>
------------------------
<span data-ttu-id="84e59-136">В этом шаблоне в фоновом режиме проверяет документов в SharePoint, чтобы определить, если они имеют значение уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="84e59-136">In this pattern, a background process checks documents in SharePoint to determine if they have a unique identifier set.</span></span> <span data-ttu-id="84e59-137">Если не уникальный идентификатор не найден в документе, фонового процесса задает уникальный идентификатор для документа.</span><span class="sxs-lookup"><span data-stu-id="84e59-137">If no unique identifier is found for a document, then the background process sets a unique identifier for the document.</span></span> <span data-ttu-id="84e59-138">Фоновый процесс делает CSOM или интерфейса API REST вызывает Присвоение уникальных идентификаторов для документов.</span><span class="sxs-lookup"><span data-stu-id="84e59-138">The background process makes CSOM or REST API calls to set unique identifiers for documents.</span></span>

- <span data-ttu-id="84e59-139">Этот шаблон выполняется по расписанию, которые определены для него.</span><span class="sxs-lookup"><span data-stu-id="84e59-139">This pattern executes according to the schedule you define for it.</span></span>
- <span data-ttu-id="84e59-140">Этот шаблон работает на все документы, которые код для обхода.</span><span class="sxs-lookup"><span data-stu-id="84e59-140">This pattern operates on all documents the code is written to crawl.</span></span>
- <span data-ttu-id="84e59-141">Мы рекомендуем вам использовать службы поиска SharePoint для выполнения запросов, включая фильтры для возвращения списка документов, не связанные с уникальными идентификаторами задавать их.</span><span class="sxs-lookup"><span data-stu-id="84e59-141">We suggest using the SharePoint search service to execute queries that include filters to return a list of documents that do not have unique identifiers set on them.</span></span>
    + <span data-ttu-id="84e59-142">Этот шаблон выполняет самого быстрого и шкал лучше, чем другие запросов шаблон.</span><span class="sxs-lookup"><span data-stu-id="84e59-142">This pattern performs the fastest and scales better than any other query pattern.</span></span>
    + <span data-ttu-id="84e59-143">Этот шаблон устраняет логика пользовательского запроса в службе фона.</span><span class="sxs-lookup"><span data-stu-id="84e59-143">This pattern eliminates custom query logic from the background service.</span></span>
    + <span data-ttu-id="84e59-144">Этот шаблон требует некоторые конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="84e59-144">This pattern requires some search configuration.</span></span>

        <span data-ttu-id="84e59-145">Дополнительные сведения о конфигурации поиска содержатся [Конфигурации поиска (SharePoint надстройки набора команд)](search-configuration-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="84e59-145">To learn more about search configuration, see the [Search Configuration (SharePoint Add-in Recipe)](search-configuration-sharepoint-add-in.md).</span></span>
- <span data-ttu-id="84e59-146">Не рекомендуется для возврата метаданных о всех документов в среде SharePoint и рекурсивно запросов с циклический перебор веб-серверы и списка объектов.</span><span class="sxs-lookup"><span data-stu-id="84e59-146">It is not recommended to recursively query and return metadata about all the documents in a SharePoint environment by looping through web and list objects.</span></span>
    + <span data-ttu-id="84e59-147">Этот шаблон выполняет медленнее всего и шкал ниже, чем любой другой запрос шаблон.</span><span class="sxs-lookup"><span data-stu-id="84e59-147">This pattern performs the slowest and scales worse than any other query pattern.</span></span>  
    + <span data-ttu-id="84e59-148">Пределы регулирования API могут возникнуть при использовании этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="84e59-148">You may encounter API throttle limits when using this pattern.</span></span>
    + <span data-ttu-id="84e59-149">Этот шаблон содержит логику пользовательского запроса в фоновом режиме службы.</span><span class="sxs-lookup"><span data-stu-id="84e59-149">This pattern includes custom query logic in the background service.</span></span>
    + <span data-ttu-id="84e59-150">Этот шаблон может быть реализован с заданием Web Azure.</span><span class="sxs-lookup"><span data-stu-id="84e59-150">This pattern may be implemented with an Azure Web Job.</span></span>

<span data-ttu-id="84e59-151">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="84e59-151">**When is it a good fit?**</span></span>

- <span data-ttu-id="84e59-152">Если вам нужно задать уникальные идентификаторы документов и удаленных приемников событий нет возможности доступны.</span><span class="sxs-lookup"><span data-stu-id="84e59-152">When you need to set unique identifiers for documents and remote event receivers are not an option available to you.</span></span>
- <span data-ttu-id="84e59-153">Если ожидается, что документы, отправленные в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="84e59-153">When you expect to have documents uploaded in bulk.</span></span>
- <span data-ttu-id="84e59-154">При необходимости для обеспечения уникальные идентификаторы документов задаются в документах.</span><span class="sxs-lookup"><span data-stu-id="84e59-154">When you need to ensure unique document IDs are set on documents.</span></span>
    + <span data-ttu-id="84e59-155">Нет возможности для приемника событий для уведомления SharePoint, если параметру идентификатор уникальный документа не удалось.</span><span class="sxs-lookup"><span data-stu-id="84e59-155">There is no way for an event receiver to notify SharePoint if setting a unique document ID failed.</span></span>
- <span data-ttu-id="84e59-156">Если вам нужно обрабатывать документы, уже хранятся в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="84e59-156">When you need to process documents already stored in SharePoint.</span></span>

<span data-ttu-id="84e59-157">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="84e59-157">**Getting Started**</span></span>

<span data-ttu-id="84e59-158">[Удаленные задания таймера (SharePoint надстройки набора команд)](remote-timer-jobs-sharepoint-add-in.md) описывается, как реализовать задания таймера удаленного в модель надстройки и предоставляет ссылки на другие статьи и примеры.</span><span class="sxs-lookup"><span data-stu-id="84e59-158">The [Remote Timer Jobs (SharePoint Add-in Recipe)](remote-timer-jobs-sharepoint-add-in.md) describes how to implement remote timer jobs in the Add-in model and provides links to several samples and articles.</span></span>

<a name="related-links"></a><span data-ttu-id="84e59-159">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="84e59-159">Related links</span></span>
=============
- [<span data-ttu-id="84e59-160">Приемники событий и приемников событий списка (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="84e59-160">Event Receivers and List Event Receivers (SharePoint Add-in Recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [<span data-ttu-id="84e59-161">Конфигурация поиска (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="84e59-161">Search Configuration (SharePoint Add-in Recipe)</span></span>](search-configuration-sharepoint-add-in.md)
- [<span data-ttu-id="84e59-162">Задания таймера удаленного (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="84e59-162">Remote Timer Jobs (SharePoint Add-in Recipe)</span></span>](remote-timer-jobs-sharepoint-add-in.md)
- <span data-ttu-id="84e59-163">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="84e59-163">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="84e59-164">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="84e59-164">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="84e59-165">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="84e59-165">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="84e59-166">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="84e59-166">Related PnP samples</span></span>
===================

- [<span data-ttu-id="84e59-167">OD4B. NavLinksInjection (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="84e59-167">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- <span data-ttu-id="84e59-168">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="84e59-168">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="84e59-169">Применимо к</span><span class="sxs-lookup"><span data-stu-id="84e59-169">Applies to</span></span>
==========
- <span data-ttu-id="84e59-170">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="84e59-170">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="84e59-171">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="84e59-171">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="84e59-172">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="84e59-172">SharePoint 2013 on-premises</span></span>
