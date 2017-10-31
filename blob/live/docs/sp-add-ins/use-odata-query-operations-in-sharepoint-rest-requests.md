---
title: "Использование операций запросов OData в запросах SharePoint REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a0cd291475b492183a57de1db2a9272154fea3f4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="use-odata-query-operations-in-sharepoint-rest-requests"></a><span data-ttu-id="97df9-102">Использование операций запросов OData в запросах SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="97df9-102">Use OData query operations in SharePoint REST requests</span></span>
<span data-ttu-id="97df9-103">Узнайте, как использовать широкий спектр операторов строки запроса OData для выбора, фильтрации и упорядочивания данных, запрашиваемых у службы REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="97df9-103">Learn how to use a wide range of OData query string operators to select, filter, and order the data you request from the SharePoint REST service.</span></span> 
 

 <span data-ttu-id="97df9-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="97df9-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

 <span data-ttu-id="97df9-107">**Перед началом работы**</span><span class="sxs-lookup"><span data-stu-id="97df9-107">**Before you start**</span></span>
 

-  [<span data-ttu-id="97df9-108">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="97df9-108">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [<span data-ttu-id="97df9-109">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="97df9-109">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
 
-  [<span data-ttu-id="97df9-110">Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="97df9-110">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
<span data-ttu-id="97df9-111">Служба REST SharePoint поддерживает широкий диапазон операторов строки запроса OData, который позволяет выбирать, фильтровать и упорядочивать запрашиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="97df9-111">The SharePoint REST service supports a wide range of OData query string operators that enable you to select, filter, and order the data you request.</span></span>
 

 <span data-ttu-id="97df9-p102">**Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="97df9-p102">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>
 


## <a name="select-fields-to-return"></a><span data-ttu-id="97df9-114">Выбор полей для возврата</span><span class="sxs-lookup"><span data-stu-id="97df9-114">Select fields to return</span></span>

<span data-ttu-id="97df9-p103">С помощью параметра запроса [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption) укажите, какие поля необходимо возвращать для списка, элемента списка или другого объекта SharePoint, представленного набором сущностей. Для возврата всех доступных полей используйте запрос `$select=*`</span><span class="sxs-lookup"><span data-stu-id="97df9-p103">Use the  [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption) query option to specify which fields to return for a given list, list item, or other SharePoint object represented by an entity set. You can use `$select=*` to return all available fields.</span></span>
 

 

 <span data-ttu-id="97df9-p104">**Примечание.** Как правило, если вы не указываете параметр запроса `$select`, служба REST возвращает все доступные поля по умолчанию. Однако иногда некоторые объекты SharePoint включают свойства, для извлечения которых требуется очень много ресурсов. Чтобы оптимизировать работу службы REST, эти свойства не включаются в запрос по умолчанию. Например, свойство **SPWeb.EffectiveBasePermissions** по умолчанию не возвращается, его необходимо запросить с помощью параметра `$select`.</span><span class="sxs-lookup"><span data-stu-id="97df9-p104">**Note**  In general, if you do not specify the  `$select` query option, the REST service returns all available fields by default. However, in a few cases, some SharePoint objects include properties that are very resource intensive to retrieve; to optimize REST service performance, these properties are not included in the default query, and must be explicitly requested.For example, the  **SPWeb.EffectiveBasePermissions** property is not returned by default, and must be explicitly requested using the `$select` query option.</span></span>
 

<span data-ttu-id="97df9-p105">Кроме того, можно сделать так, чтобы возвращались планируемые поля из других списков и значения подстановки. Для этого укажите имя поля в параметрах запроса `$select` и `$expand`. Пример:</span><span class="sxs-lookup"><span data-stu-id="97df9-p105">In addition, you can specify that the request returns projected fields from other lists and the values of lookups. To do this, specify the field name in both the  `$select` and `$expand` query options. For example:</span></span>
 

 
 `http://server/site/_api/web/lists('guid')/items?$select=Title,Products/Name&amp;$expand=Products/Name`
 

 
<span data-ttu-id="97df9-122">Массовое расширение и выбор связанных элементов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="97df9-122">Bulk expansion and selection of related items is not supported.</span></span>
 

 

## <a name="select-items-to-return"></a><span data-ttu-id="97df9-123">Выбор элементов для возврата</span><span class="sxs-lookup"><span data-stu-id="97df9-123">Select items to return</span></span>

<span data-ttu-id="97df9-p106">С помощью параметра запроса [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption) укажите, какие элементы необходимо возвращать. В разделе [Операторы запросов OData, поддерживаемые в службе SharePoint REST](#bk_supported) указаны параметры сравнения и функции для фильтрации запросов, которые можно использовать в службе SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="97df9-p106">Use the  [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption) query option to select which items to return. [OData query operators supported in the SharePoint REST service](#bk_supported) lists the filter query comparison options and functions you can use with the SharePoint REST service.</span></span>
 

 

## <a name="query-for-single-value-lookup-fields"></a><span data-ttu-id="97df9-126">Запрос полей подстановки с одним значением</span><span class="sxs-lookup"><span data-stu-id="97df9-126">Query for single value lookup fields</span></span>

<span data-ttu-id="97df9-p107">Поля подстановки одиночного значения представлены двумя отдельными полями в службе REST SharePoint: одно поле представляет фактическое значение поля, а другое — имя поля. Вы можете выполнять запросы значения поля подстановки так же, как для любого другого поля этого типа данных. Например, если значением поля подстановки является строка, вы можете использовать в вашем запросе параметры сравнения строк.</span><span class="sxs-lookup"><span data-stu-id="97df9-p107">Single value lookup fields are represented by two separate fields in the SharePoint REST service: one field representing the actual field value, and another representing the field name. You can perform queries against the lookup field value as you would any other field of that data type. For example, if the lookup field value is a string, you can use string comparison options in your query.</span></span>
 

 

## <a name="query-for-users"></a><span data-ttu-id="97df9-130">Запрос пользователей</span><span class="sxs-lookup"><span data-stu-id="97df9-130">Query for users</span></span>

<span data-ttu-id="97df9-p108">В службе REST SharePoint пользователи представлены понятным (отображаемым) именем пользователя, а не их псевдонимами или комбинацией домена и псевдонима. Следовательно, вам необходимо сформировать запросы к понятным именам пользователей.</span><span class="sxs-lookup"><span data-stu-id="97df9-p108">In the SharePoint REST service, users are represented by the user's friendly (display) name, and not their alias or domain\alias combination. Therefore, you must construct user queries against users' friendly names.</span></span>
 

 

 <span data-ttu-id="97df9-133">**Примечание.** Запросы пользователей на основе участия в группах не поддерживаются. Использование оператора **Current** для выполнения запросов по идентификатору текущего пользователя не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="97df9-133">**Note**  Membership-based user queries are not supported.Usage of the  **Current** operator to do queries using the ID of the current user is not supported.</span></span>
 


## <a name="query-for-multi-value-lookup-fields-and-users"></a><span data-ttu-id="97df9-134">Запрос полей подстановки с несколькими значениями и пользователей</span><span class="sxs-lookup"><span data-stu-id="97df9-134">Query for multi-value lookup fields and users</span></span>

<span data-ttu-id="97df9-135">Так как поля подстановки с несколькими значениями возвращаются в виде строки из нескольких значений, то их нельзя запросить (например, эквивалент элемента **Includes** или элемента **NotIncludes** не поддерживается).</span><span class="sxs-lookup"><span data-stu-id="97df9-135">Because multi-value lookup fields are returned as a string of multiple values, there is no way to query for them (for example, the equivalent of an  **Includes** element or **NotIncludes** element is not supported).</span></span>
 

 

## <a name="sort-returned-items"></a><span data-ttu-id="97df9-136">Сортировка результатов</span><span class="sxs-lookup"><span data-stu-id="97df9-136">Sort returned items</span></span>

<span data-ttu-id="97df9-p109">Используйте параметр [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption), чтобы указать, как сортировать результаты запроса. Чтобы сортировать результаты по нескольким полям, укажите список полей через запятую. Вы также можете указать, в каком порядке нужно сортировать элементы (по возрастанию или по убыванию), добавив к запросу ключевое слово **asc** или **desc**.</span><span class="sxs-lookup"><span data-stu-id="97df9-p109">Use the  [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption) query option to specify how to sort the items in your query return set. To sort by multiple fields, specify a comma-separated list of fields. You can also specify whether to sort the items in ascending or descending order by appending the **asc** or **desc** keyword to your query.</span></span>
 

 

## <a name="page-through-returned-items"></a><span data-ttu-id="97df9-140">Постраничное разбиение результатов</span><span class="sxs-lookup"><span data-stu-id="97df9-140">Page through returned items</span></span>

<span data-ttu-id="97df9-141">С помощью параметров [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) и [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx) выберите часть элементов, которую нужно исключить из результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="97df9-141">Use the  [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) and [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx) query options to select a subset of the items that would otherwise be returned by your query.</span></span>
 

 

 <span data-ttu-id="97df9-142">**Примечание.** Параметр $skip не работает с запросами, касающимися элементов списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="97df9-142">**Note**  The $skip query option does not work with queries for SharePoint list items.</span></span>
 

<span data-ttu-id="97df9-p110">Параметр  `$top` позволяет выбрать первые *n*  элементов набора возврата для получения. Например, следующий URI запрашивает возврат только первых десяти элементов из потенциального набора результатов:</span><span class="sxs-lookup"><span data-stu-id="97df9-p110">The  `$top` option enables you to select the first *n*  items of the return set for return. For example, the following URI requests that only the first ten items in the prospective return set actually be returned:</span></span>
 

 
 `http://server/site/_api/web/lists('<guid>')/items$top=10`
 

 
<span data-ttu-id="97df9-145">Параметр $skiptoken позволяет пропустить указанное количество элементов и получить остальные.</span><span class="sxs-lookup"><span data-stu-id="97df9-145">The $skiptoken option enables you to skip over items until the specified item is reached and return the rest.</span></span>
 

 
 `$skiptoken=Paged=TRUE&amp;p_ID=5`
 

 

 <span data-ttu-id="97df9-p111">**Примечание.** При использовании этих параметров запроса следует учитывать, что постраничное разбиение в OData выполняется по порядку. Предположим, что вы размещаете кнопку следующей страницы для отображения элементов списка SharePoint. Вы используете службу REST, чтобы кнопка возвращала элементы 1–20, затем элементы 21–40 и так далее. Однако предположим, что другой пользователь удаляет элемент 4 и 18 между нажатиями кнопки "Далее". В этом случае порядковое размещение остальных элементов сбрасывается, и при отображении элементов 21–40 пропускаются два элемента.</span><span class="sxs-lookup"><span data-stu-id="97df9-p111">**Note**  When using these query options, take into account that paging in OData is ordinal. For example, suppose you are implementing a next page button to display SharePoint list items. You use the REST service to enable the button to return items 1 through 20 when clicked, then items 21 through 40, and so on. However, suppose another user deletes items 4 and 18 between clicks of the next button. In such a case, the ordinal positioning of the remaining items is reset, and displaying items 21 through 40 actually skips over two items.</span></span>
 


## <a name="odata-query-operators-supported-in-the-sharepoint-rest-service"></a><span data-ttu-id="97df9-151">Операторы запросов OData, поддерживаемые в службе SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="97df9-151">OData query operators supported in the SharePoint REST service</span></span>
<span data-ttu-id="97df9-152"><a name="bk_supported"> </a></span><span class="sxs-lookup"><span data-stu-id="97df9-152"></span></span>



|<span data-ttu-id="97df9-153">**Поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="97df9-153">**Supported**</span></span>|<span data-ttu-id="97df9-154">**Не поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="97df9-154">**Not supported**</span></span>|
|:-----|:-----|
|<span data-ttu-id="97df9-155">**Числовые сравнения** Lt Le Gt Ge Eq Ne</span><span class="sxs-lookup"><span data-stu-id="97df9-155">**Numeric comparisons** Lt Le Gt Ge Eq Ne</span></span>| <span data-ttu-id="97df9-156">Арифметические операторы (Add, Sub, Mul, Div, Mod) Базовые математические функции (округление, пол, потолок)</span><span class="sxs-lookup"><span data-stu-id="97df9-156">Arithmetic operators  (Add, Sub, Mul, Div, Mod) Basic math functions (round, floor, ceiling)</span></span> |
|<span data-ttu-id="97df9-157">**Сравнение строк** startsWith substringof Eq Ne</span><span class="sxs-lookup"><span data-stu-id="97df9-157">**String comparisons** startsWith substringof Eq Ne</span></span>| <span data-ttu-id="97df9-158">endsWith replace substring tolower toupper trim concat</span><span class="sxs-lookup"><span data-stu-id="97df9-158">endsWith replace substring tolower toupper trim concat</span></span>|
|<span data-ttu-id="97df9-159">**Функции даты и времени** day() month() year() hour() minute() second()</span><span class="sxs-lookup"><span data-stu-id="97df9-159">**Date and time functions** day() month() year() hour() minute() second()</span></span>| <span data-ttu-id="97df9-160">Оператор DateTimeRangesOverlap Запросы относительно того, относится ли дата и время к временному шаблону</span><span class="sxs-lookup"><span data-stu-id="97df9-160">DateTimeRangesOverlap operator Querying as to whether a date time falls inside a recurrent date time pattern</span></span>|
<span data-ttu-id="97df9-161">На следующем рисунке показаны поддерживаемые параметры запроса OData.</span><span class="sxs-lookup"><span data-stu-id="97df9-161">The figure below shows the supported OData query options.</span></span>
 

 

<span data-ttu-id="97df9-162">**Поддерживаемые параметры запроса OData**</span><span class="sxs-lookup"><span data-stu-id="97df9-162">**Supported OData query options**</span></span>

 

 
![Синтаксис параметров запроса службы SharePoint REST](../images/SPF15Con_REST_queryOptionSyntax.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="97df9-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="97df9-164">Additional resources</span></span>
<span data-ttu-id="97df9-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="97df9-165"></span></span>


-  [<span data-ttu-id="97df9-166">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="97df9-166">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [<span data-ttu-id="97df9-167">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="97df9-167">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="97df9-168">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="97df9-168">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
    
 
-  [<span data-ttu-id="97df9-169">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="97df9-169">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
    
 
-  [<span data-ttu-id="97df9-170">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="97df9-170">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
 
-  [<span data-ttu-id="97df9-171">Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="97df9-171">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
-  [<span data-ttu-id="97df9-172">Справочные материалы по интерфейсу API службы REST и примеры</span><span class="sxs-lookup"><span data-stu-id="97df9-172">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 

 

 
