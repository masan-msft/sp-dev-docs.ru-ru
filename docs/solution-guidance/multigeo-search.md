---
title: "Поиск в SharePoint несколькими географически клиентов"
ms.date: 11/03/2017
ms.openlocfilehash: 214c1b7ca1a6e2b985f1be780c29ea8b34165ef0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="search-in-a-multi-geo-sharepoint-tenant"></a><span data-ttu-id="78bdd-102">Поиск в SharePoint несколькими географически клиентов</span><span class="sxs-lookup"><span data-stu-id="78bdd-102">Search in a Multi-Geo SharePoint tenant</span></span>

> <span data-ttu-id="78bdd-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="78bdd-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="78bdd-104">В географически несколькими SharePoint для клиентов каждого географически из индекса поиска, а также собственный центр независимой поиска.</span><span class="sxs-lookup"><span data-stu-id="78bdd-104">In a Multi-Geo SharePoint tenant, each geo location has its own search index, as well as its own independent search center.</span></span> <span data-ttu-id="78bdd-105">По умолчанию при настройке центра поиска, центра поиска использует следующий шаблон URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="78bdd-105">By default, when you configure a search center, the search center uses the following URL pattern.</span></span>

```
https://<tenanturl>.sharepoint.com/sites/search
```

<span data-ttu-id="78bdd-106">В данном примере показано на следующем рисунке несколькими географически клиент имеет географически расположениях, каждый из которых поиска для конкретных расположение географически URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="78bdd-106">In the scenario shown in the following image, a Multi-Geo tenant has three geo locations, each with a geo location-specific search URL.</span></span>

|<span data-ttu-id="78bdd-107">**Географического расположения**</span><span class="sxs-lookup"><span data-stu-id="78bdd-107">**Geo location**</span></span>|<span data-ttu-id="78bdd-108">**URL-адрес поиска**</span><span class="sxs-lookup"><span data-stu-id="78bdd-108">**Search URL**</span></span>|
|:---------------|:-------------|
|<span data-ttu-id="78bdd-109">Северная Америка (расположение по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="78bdd-109">North America (default location)</span></span>|<span data-ttu-id="78bdd-110">https://contoso.SharePoint.com/Search</span><span class="sxs-lookup"><span data-stu-id="78bdd-110">https://contoso.sharepoint.com/search</span></span>|
|<span data-ttu-id="78bdd-111">Европа (расположение вспомогательных)</span><span class="sxs-lookup"><span data-stu-id="78bdd-111">Europe (satellite location)</span></span>|<span data-ttu-id="78bdd-112">https://contosoeur.SharePoint.com/Search</span><span class="sxs-lookup"><span data-stu-id="78bdd-112">https://contosoeur.sharepoint.com/search</span></span>|
|<span data-ttu-id="78bdd-113">Азиатско-тихоокеанский (расположение вспомогательных)</span><span class="sxs-lookup"><span data-stu-id="78bdd-113">Asia (satellite location)</span></span>|<span data-ttu-id="78bdd-114">https://contosoapc.SharePoint.com/Search</span><span class="sxs-lookup"><span data-stu-id="78bdd-114">https://contosoapc.sharepoint.com/search</span></span>|


![Отображение URL-адреса сайтов географического расположения в Северной Америке, Европе и Азии с поиска для конкретных клиентов Карта мира](media/multigeo/multigeosearch_intro.png)

<span data-ttu-id="78bdd-116">Из конечного пользователя точки зрения поиска пределах текущего географического расположения.</span><span class="sxs-lookup"><span data-stu-id="78bdd-116">From an end user point of view, search is scoped to the current geo location.</span></span> <span data-ttu-id="78bdd-117">При выполнении пользователями поиска с сайта, размещенного в Северной Америке, они будут видеть только результаты из расположения географически Северная Америка.</span><span class="sxs-lookup"><span data-stu-id="78bdd-117">When users perform searches from a site hosted in North America, they will only see results from the North America geo location.</span></span> <span data-ttu-id="78bdd-118">Операций поиска с сайта, размещенного в Европе возвращает результаты из сайтов в расположении географически Европе.</span><span class="sxs-lookup"><span data-stu-id="78bdd-118">Searches from a site hosted in Europe will return results from sites in the Europe geo location.</span></span>

> [!NOTE] 
> <span data-ttu-id="78bdd-119">В будущем поиска будут Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="78bdd-119">In the future, search will be Multi-Geo aware.</span></span> <span data-ttu-id="78bdd-120">Запрос поиска, запустите из любого места в пределах клиента будет найти все, что географического расположения в клиента и возвращается объединенных результатов.</span><span class="sxs-lookup"><span data-stu-id="78bdd-120">A search query run from any location within the tenant will search all geo locations within the tenant and return combined results.</span></span>

## <a name="working-with-search-programmatically-in-a-multi-geo-tenant"></a><span data-ttu-id="78bdd-121">Работа с поиска программными средствами в географически нескольких клиентов</span><span class="sxs-lookup"><span data-stu-id="78bdd-121">Working with search programmatically in a Multi-Geo tenant</span></span>
<span data-ttu-id="78bdd-122">Программная работа с поиском аналогично интерфейса поиска конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="78bdd-122">Working with search programmatically is similar to the end user search experience.</span></span> <span data-ttu-id="78bdd-123">При выполнении запроса поиска, вы получите только результаты для географического расположения, в котором при выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="78bdd-123">If you perform a search query, you'll only get results for the geo location in which you run the query.</span></span> <span data-ttu-id="78bdd-124">Приложений тем не менее, можно выполнять поиск клиента несколькими географически.</span><span class="sxs-lookup"><span data-stu-id="78bdd-124">Your applications can, however, perform Multi-Geo tenant searches.</span></span> <span data-ttu-id="78bdd-125">Для этого итерации по географического расположения клиента, выдачу того же запроса поиска в каждом расположении географически и затем объедините результаты.</span><span class="sxs-lookup"><span data-stu-id="78bdd-125">To do this, iterate over the geo locations in your tenant, issue the same search query in each geo location, and then concatenate the results.</span></span>

<span data-ttu-id="78bdd-126">Этот подход может быть достаточно для в некоторых сценариях (например, поиска для сайтов данного типа).</span><span class="sxs-lookup"><span data-stu-id="78bdd-126">This approach might be sufficient for in some scenarios (for example, searches for sites of a given type).</span></span> <span data-ttu-id="78bdd-127">Тем не менее в некоторых случаях требуется для ранжирования по релевантности результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="78bdd-127">However, in some cases, you want the search results to be ranked according to relevancy.</span></span> <span data-ttu-id="78bdd-128">Это невозможно при наличии нескольких наборов результатов.</span><span class="sxs-lookup"><span data-stu-id="78bdd-128">You can't do this when you have multiple result sets.</span></span> <span data-ttu-id="78bdd-129">Если для сценария требуется ранжирования поиска, необходимо будет Подождите, пока взаимодействия с несколькими географически доступен.</span><span class="sxs-lookup"><span data-stu-id="78bdd-129">If your scenario requires search ranking, you will need to wait until a Multi-Geo search experience is available.</span></span>


## <a name="see-also"></a><span data-ttu-id="78bdd-130">См. также</span><span class="sxs-lookup"><span data-stu-id="78bdd-130">See also</span></span>

- [<span data-ttu-id="78bdd-131">Управление центра поиска в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="78bdd-131">Manage the Search Center in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-the-Search-Center-in-SharePoint-Online-174d36e0-2f85-461a-ad9a-8b3f434a4213?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="78bdd-132">Обзор поиска в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="78bdd-132">Overview of search in SharePoint Online</span></span>](https://support.office.com/en-us/article/Overview-of-search-in-SharePoint-Online-479cfd6b-900b-46aa-b497-c13787771d3f?ui=en-US&rs=en-US&ad=US)
