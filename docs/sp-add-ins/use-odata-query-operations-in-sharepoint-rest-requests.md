---
title: "Использование операций запросов OData в запросах REST SharePoint"
description: "Узнайте, как использовать широкий спектр операторов строки запроса OData для выбора, фильтрации и упорядочивания данных, запрашиваемых у службы REST SharePoint."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 404559d6acfa97bdd9b779e625b4badebdcd6c6a
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="use-odata-query-operations-in-sharepoint-rest-requests"></a><span data-ttu-id="681c3-103">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="681c3-103">Use OData query operations in SharePoint REST requests</span></span>

<span data-ttu-id="681c3-104">**Перед началом работы**</span><span class="sxs-lookup"><span data-stu-id="681c3-104">**Before you start**</span></span>

- [<span data-ttu-id="681c3-105">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="681c3-105">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="681c3-106">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="681c3-106">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
- [<span data-ttu-id="681c3-107">Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="681c3-107">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)

<span data-ttu-id="681c3-108">Служба REST SharePoint поддерживает широкий диапазон операторов строки запроса OData, который позволяет выбирать, фильтровать и упорядочивать запрашиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="681c3-108">The SharePoint REST service supports a wide range of OData query string operators that enable you to select, filter, and order the data you request.</span></span>
 
> [!TIP] 
> <span data-ttu-id="681c3-p101">Служба REST SharePoint Online (а также локальной среды SharePoint 2016 и более поздних версий) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData `$batch`. Дополнительные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="681c3-p101">`$batch`  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  [](make-batch-requests-with-the-rest-apis.md) query option. For details and links to code samples, see Make batch requests with the REST APIs.</span></span>

## <a name="select-fields-to-return"></a><span data-ttu-id="681c3-111">Выбор полей для возврата</span><span class="sxs-lookup"><span data-stu-id="681c3-111">Select fields to return</span></span>

<span data-ttu-id="681c3-p102">С помощью параметра запроса [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption) укажите, какие поля необходимо возвращать для списка, элемента списка или другого объекта SharePoint, представленного набором сущностей. Для возврата всех доступных полей используйте запрос `$select=*`.</span><span class="sxs-lookup"><span data-stu-id="681c3-p102">Use the  [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption) query option to specify which fields to return for a given list, list item, or other SharePoint object represented by an entity set. You can use `$select=*` to return all available fields.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="681c3-114">Как правило, если вы не указываете параметр запроса `$select`, служба REST по умолчанию возвращает все доступные поля.</span><span class="sxs-lookup"><span data-stu-id="681c3-114">In general, if you do not specify the  `$select` query option, the REST service returns all available fields by default.</span></span> <span data-ttu-id="681c3-115">Но иногда некоторые объекты SharePoint включают свойства, для получения которых требуется очень много ресурсов. Для оптимизации работы службы REST эти свойства не включаются в запрос по умолчанию. Их следует запрашивать специально. Например, свойство **SPWeb.EffectiveBasePermissions** по умолчанию не возвращается, его необходимо запросить с помощью параметра запроса `$select`.</span><span class="sxs-lookup"><span data-stu-id="681c3-115">However, in a few cases, some SharePoint objects include properties that are very resource intensive to retrieve; to optimize REST service performance, these properties are not included in the default query, and must be explicitly requested.For example, the  **SPWeb.EffectiveBasePermissions** property is not returned by default, and must be explicitly requested using the `$select` query option.</span></span>

<span data-ttu-id="681c3-p104">Кроме того, можно сделать так, чтобы возвращались планируемые поля из других списков и значения подстановки. Для этого укажите имя поля в параметрах запроса `$select` и `$expand`. Пример:</span><span class="sxs-lookup"><span data-stu-id="681c3-p104">In addition, you can specify that the request returns projected fields from other lists and the values of lookups. To do this, specify the field name in both the  `$select` and `$expand` query options. For example:</span></span>

`http://server/site/_api/web/lists('guid')/items?$select=Title,Products/Name&amp;$expand=Products/Name`

<span data-ttu-id="681c3-119">Массовое расширение и выбор связанных элементов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="681c3-119">Bulk expansion and selection of related items is not supported.</span></span>

## <a name="select-items-to-return"></a><span data-ttu-id="681c3-120">Выбор элементов для возврата</span><span class="sxs-lookup"><span data-stu-id="681c3-120">Select items to return</span></span>

<span data-ttu-id="681c3-p105">С помощью параметра запроса [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption) укажите, какие элементы необходимо возвращать. В разделе [Операторы запросов OData, поддерживаемые в службе SharePoint REST](#bk_supported) указаны параметры сравнения и функции для фильтрации запросов, которые можно использовать в службе SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="681c3-p105">Use the  [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption) query option to select which items to return. [OData query operators supported in the SharePoint REST service](#bk_supported) lists the filter query comparison options and functions you can use with the SharePoint REST service.</span></span>

## <a name="query-for-single-value-lookup-fields"></a><span data-ttu-id="681c3-123">Запрос полей подстановки с одним значением</span><span class="sxs-lookup"><span data-stu-id="681c3-123">Query for single value lookup fields</span></span>

<span data-ttu-id="681c3-p106">Поля подстановки одиночного значения представлены двумя отдельными полями в службе REST SharePoint: одно поле представляет фактическое значение поля, а другое — имя поля. Вы можете выполнять запросы значения поля подстановки так же, как для любого другого поля этого типа данных. Например, если значением поля подстановки является строка, вы можете использовать в вашем запросе параметры сравнения строк.</span><span class="sxs-lookup"><span data-stu-id="681c3-p106">Single value lookup fields are represented by two separate fields in the SharePoint REST service: one field representing the actual field value, and another representing the field name. You can perform queries against the lookup field value as you would any other field of that data type. For example, if the lookup field value is a string, you can use string comparison options in your query.</span></span>

## <a name="query-for-users"></a><span data-ttu-id="681c3-127">Запрос пользователей</span><span class="sxs-lookup"><span data-stu-id="681c3-127">Query for users</span></span>

<span data-ttu-id="681c3-p107">В службе REST SharePoint пользователи представлены понятным (отображаемым) именем пользователя, а не их псевдонимами или комбинацией домена и псевдонима. Следовательно, вам необходимо сформировать запросы к понятным именам пользователей.</span><span class="sxs-lookup"><span data-stu-id="681c3-p107">In the SharePoint REST service, users are represented by the user's friendly (display) name, and not their alias or domain\alias combination. Therefore, you must construct user queries against users' friendly names.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="681c3-130">Запросы на получение пользователей с учетом членства в группах не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="681c3-130">Membership-based user queries are not supported.</span></span> <span data-ttu-id="681c3-131">Использование оператора **Current** для выполнения запросов с использованием идентификатора текущего пользователя не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="681c3-131">Usage of the **Current** operator to do queries using the ID of the current user is not supported.</span></span>

## <a name="query-for-multi-value-lookup-fields-and-users"></a><span data-ttu-id="681c3-132">Запрос на получение полей подстановки с несколькими значениями и пользователей</span><span class="sxs-lookup"><span data-stu-id="681c3-132">Query for multi-value lookup fields and users</span></span>

<span data-ttu-id="681c3-133">Поскольку поля подстановки с несколькими значениями возвращаются как строка из нескольких значений, то их нельзя запросить (например, эквивалент элемента **Includes** или элемента **NotIncludes** не поддерживается).</span><span class="sxs-lookup"><span data-stu-id="681c3-133">Because multi-value lookup fields are returned as a string of multiple values, there is no way to query for them (for example, the equivalent of an **Includes** element or **NotIncludes** element is not supported).</span></span>

## <a name="sort-returned-items"></a><span data-ttu-id="681c3-134">Сортировка результатов</span><span class="sxs-lookup"><span data-stu-id="681c3-134">Sort returned items</span></span>

<span data-ttu-id="681c3-135">Используйте параметр [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption), чтобы указать, как нужно сортировать результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="681c3-135">Use the [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption) query option to specify how to sort the items in your query return set.</span></span> <span data-ttu-id="681c3-136">Чтобы сортировать результаты по нескольким полям, укажите список полей через запятую.</span><span class="sxs-lookup"><span data-stu-id="681c3-136">To sort by multiple fields, specify a comma-separated list of fields.</span></span> <span data-ttu-id="681c3-137">Вы также можете указать, в каком порядке нужно сортировать элементы (по возрастанию или по убыванию), добавив к запросу ключевое слово **asc** или **desc**.</span><span class="sxs-lookup"><span data-stu-id="681c3-137">Use the  $orderby query option to specify how to sort the items in your query return set. To sort by multiple fields, specify a comma-separated list of fields. You can also specify whether to sort the items in ascending or descending order by appending the **asc** or **desc** keyword to your query.</span></span>

## <a name="page-through-returned-items"></a><span data-ttu-id="681c3-138">Постраничное разбиение результатов</span><span class="sxs-lookup"><span data-stu-id="681c3-138">Page through returned items</span></span>

<span data-ttu-id="681c3-139">С помощью параметров запроса [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) и [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx) выберите часть элементов, которую нужно исключить из результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="681c3-139">Use the  [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) and [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx) query options to select a subset of the items that would otherwise be returned by your query.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="681c3-140">Параметр запроса $skip не работает с запросами для элементов списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="681c3-140">The $skip query option does not work with queries for SharePoint list items.</span></span>

<span data-ttu-id="681c3-141">Параметр `$top` позволяет выбрать первые *n* результатов для возврата.</span><span class="sxs-lookup"><span data-stu-id="681c3-141">The  `$top` option enables you to select the first *n*  items of the return set for return. For example, the following URI requests that only the first ten items in the prospective return set actually be returned:</span></span> <span data-ttu-id="681c3-142">Например, с помощью следующего универсального кода ресурса (URI) можно запросить возврат только первых десяти результатов:</span><span class="sxs-lookup"><span data-stu-id="681c3-142">The   option enables you to select the first   items of the return set for return. For example, the following URI requests that only the first ten items in the prospective return set actually be returned:</span></span>

`http://server/site/_api/web/lists('<guid>')/items$top=10`

<span data-ttu-id="681c3-143">Параметр $skiptoken позволяет пропустить указанное количество элементов и получить остальные.</span><span class="sxs-lookup"><span data-stu-id="681c3-143">The $skiptoken option enables you to skip over items until the specified item is reached and return the rest.</span></span>

`$skiptoken=Paged=TRUE&amp;p_ID=5`
 
> [!NOTE] 
> <span data-ttu-id="681c3-144">При использовании этих параметров запроса следует учитывать, что постраничное разбиение в OData выполняется по порядку.</span><span class="sxs-lookup"><span data-stu-id="681c3-144">When using these query options, take into account that paging in OData is ordinal.</span></span> <span data-ttu-id="681c3-145">Предположим, что вы размещаете кнопку следующей страницы для отображения элементов списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="681c3-145">For example, suppose you are implementing a next page button to display SharePoint list items.</span></span> <span data-ttu-id="681c3-146">Вы используете службу REST, чтобы кнопка возвращала элементы 1–20, элементы 21–40 и так далее.</span><span class="sxs-lookup"><span data-stu-id="681c3-146">You use the REST service to enable the button to return items 1 through 20 when clicked, and then items 21 through 40, and so on.</span></span> <span data-ttu-id="681c3-147">Однако предположим, что другой пользователь удаляет элемент 4 и 18 между нажатиями кнопки "Далее".</span><span class="sxs-lookup"><span data-stu-id="681c3-147">However, suppose another user deletes items 4 and 18 between clicks of the next button.</span></span> <span data-ttu-id="681c3-148">В этом случае порядковое размещение остальных элементов сбрасывается, и при отображении элементов 21–40 пропускаются два элемента.</span><span class="sxs-lookup"><span data-stu-id="681c3-148">In such a case, the ordinal positioning of the remaining items is reset, and displaying items 21 through 40 actually skips over two items.</span></span>
 
<span data-ttu-id="681c3-149"><a name="bk_supported"> </a></span><span class="sxs-lookup"><span data-stu-id="681c3-149"></span></span>

## <a name="odata-query-operators-supported-in-the-sharepoint-rest-service"></a><span data-ttu-id="681c3-150">Операторы запросов OData, поддерживаемые в службе SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="681c3-150">OData query operators supported in the SharePoint REST service</span></span>

|<span data-ttu-id="681c3-151">**Поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="681c3-151">**Supported**</span></span>|<span data-ttu-id="681c3-152">**Не поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="681c3-152">**Not supported**</span></span>|
|:-----|:-----|
|<span data-ttu-id="681c3-153">**Числовые сравнения** Lt Le Gt Ge Eq Ne</span><span class="sxs-lookup"><span data-stu-id="681c3-153">**Numeric comparisons** Lt Le Gt Ge Eq Ne</span></span>| <span data-ttu-id="681c3-154">**Арифметические операторы** (Add, Sub, Mul, Div, Mod)</span><span class="sxs-lookup"><span data-stu-id="681c3-154">Arithmetic operators           (Add, Sub, Mul, Div, Mod)</span></span><br/><span data-ttu-id="681c3-155">**Базовые математические функции** (округление, пол, потолок)</span><span class="sxs-lookup"><span data-stu-id="681c3-155">Basic math functions          (round, floor, ceiling)</span></span> |
|<span data-ttu-id="681c3-156">**Сравнение строк** startsWith substringof Eq Ne</span><span class="sxs-lookup"><span data-stu-id="681c3-156">**String comparisons** startsWith substringof Eq Ne</span></span>| <span data-ttu-id="681c3-157">endsWith replace substring tolower toupper trim concat</span><span class="sxs-lookup"><span data-stu-id="681c3-157">endsWith replace substring tolower toupper trim concat</span></span>|
|<span data-ttu-id="681c3-158">**Функции даты и времени** day() month() year() hour() minute() second()</span><span class="sxs-lookup"><span data-stu-id="681c3-158">**Date and time functions** day() month() year() hour() minute() second()</span></span>| <span data-ttu-id="681c3-159">Оператор DateTimeRangesOverlap</span><span class="sxs-lookup"><span data-stu-id="681c3-159">DateTimeRangesOverlap operator</span></span><br/><span data-ttu-id="681c3-160">Выполнение запроса для выяснения того, входит ли дата или время в указанный повторяющийся временной интервал</span><span class="sxs-lookup"><span data-stu-id="681c3-160">Querying as to whether a date time falls inside a recurrent date time pattern</span></span>|

<span data-ttu-id="681c3-161">Ниже показаны поддерживаемые параметры запроса OData.</span><span class="sxs-lookup"><span data-stu-id="681c3-161">The figure below shows the supported OData query options.</span></span>

<span data-ttu-id="681c3-162">**Поддерживаемые параметры запроса OData**</span><span class="sxs-lookup"><span data-stu-id="681c3-162">**Supported OData query options**</span></span>

![Синтаксис параметров запроса для службы REST SharePoint](../images/SPF15Con_REST_queryOptionSyntax.png)

<br/>

## <a name="see-also"></a><span data-ttu-id="681c3-164">См. также</span><span class="sxs-lookup"><span data-stu-id="681c3-164">See also</span></span>
<span data-ttu-id="681c3-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="681c3-165"></span></span>

- [<span data-ttu-id="681c3-166">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="681c3-166">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="681c3-167">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="681c3-167">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [<span data-ttu-id="681c3-168">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="681c3-168">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="681c3-169">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="681c3-169">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 

 

 
