---
title: "Справочник по API-Интерфейс REST BCS для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 364fb8d7-87d9-4be7-affd-90caba3cd0c0
ms.openlocfilehash: f33adf455a216d1a7dba82832d9bcf7051068cb0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="bcs-rest-api-reference-for-sharepoint"></a><span data-ttu-id="a8010-102">Справочник по API-Интерфейс REST BCS для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-102">BCS REST API reference for SharePoint</span></span>

  
    
    
![Ссылки и библиотеки класса](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="a8010-104">Содержит сведения о создании представлений состояния (REST) URL-адреса для доступа и работы с внешними источниками данных с помощью Business Connectivity Services (BCS) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8010-104">Contains reference information for constructing Representational State Transfer (REST) URLs to access and manipulate external data sources using Business Connectivity Services (BCS) in SharePoint.</span></span>
## <a name="using-restful-apis-to-access-external-data-in-sharepoint"></a><span data-ttu-id="a8010-105">Использование интерфейсов API RESTful для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-105">Using RESTful APIs to access external data in SharePoint</span></span>
<span data-ttu-id="a8010-106"><a name="bkmk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="a8010-106"></span></span>

<span data-ttu-id="a8010-107">Интерфейс REST, предоставляемых SharePoint позволяет получить доступ к большинству ресурсов SharePoint через специально созданный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8010-107">The REST interface provided by SharePoint enables you to access most SharePoint resources through specially constructed URLs.</span></span> <span data-ttu-id="a8010-108">Эта архитектура использует Business Connectivity Services (BCS) для предоставления доступа к внешним данным.</span><span class="sxs-lookup"><span data-stu-id="a8010-108">Business Connectivity Services (BCS) uses this architecture to provide access to external data.</span></span>
  
    
    
<span data-ttu-id="a8010-109">Так же, как и для доступа к элементам списка стандартных можно приступить к внешним данным с построения URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="a8010-109">You can access external data by constructing URLs just as you would to access standard list items.</span></span>
  
    
    

> <span data-ttu-id="a8010-110">**Примечание:** Доступ к сущностей через BDC непосредственно не указан.</span><span class="sxs-lookup"><span data-stu-id="a8010-110">**Note:** Access to entities through the BDC directly is not provided.</span></span> <span data-ttu-id="a8010-111">Для работы с внешними данными, необходимо создать внешний список и использовать URL-адреса REST для доступа к элементам списка, содержащихся во внешнем списке.</span><span class="sxs-lookup"><span data-stu-id="a8010-111">To work with external data, you must create an external list and use the REST URLs to access the list items contained in the external list.</span></span> 
  
    
    

<span data-ttu-id="a8010-112">Поддерживаемые HTTP-команды для работы с внешними списками, **GET**, **PUT**, **POST**и **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="a8010-112">The supported HTTP verbs for working with external lists are **GET**, **PUT**, **POST**, and **DELETE**.</span></span>
  
    
    
<span data-ttu-id="a8010-p103">В отличие от обычных списками невозможно создать внешний список, использующий REST. Необходимо выполнить, путем создания модели BDC и внешнего списка с помощью Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="a8010-p103">Unlike with normal lists, you can't create an external list using REST. You must do that by creating a BDC model and an external list using Visual Studio 2012.</span></span>
  
    
    
<span data-ttu-id="a8010-115">Сведения, приведенные в таблице 1 показано, как для создания URL-адреса REST и соответствующие вызовы объектной модели клиента для доступа и работы с данными из внешних источников данных.</span><span class="sxs-lookup"><span data-stu-id="a8010-115">The information in Table 1 shows how to construct RESTful URLs and the corresponding client object model calls to access and manipulate data from external data sources.</span></span>
  
    
    

<span data-ttu-id="a8010-116">**В таблице 1. RESTful форматы URL-адрес для доступа к внешним данным**</span><span class="sxs-lookup"><span data-stu-id="a8010-116">**Table 1. RESTful URL formats for accessing external data**</span></span>


|<span data-ttu-id="a8010-117">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="a8010-117">**URL**</span></span>|<span data-ttu-id="a8010-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a8010-118">**Description**</span></span>|<span data-ttu-id="a8010-119">**Метод HTTP**</span><span class="sxs-lookup"><span data-stu-id="a8010-119">**HTTP method**</span></span>|
|:-----|:-----|:-----|
| `http://[sharepointsite]/_api` <br/> |<span data-ttu-id="a8010-p104">Базовое все запросы REST. В виртуальном каталоге _api сопоставляется позвонить в client.svc, где используется клиентская объектная модель.</span><span class="sxs-lookup"><span data-stu-id="a8010-p104">The base of any REST request. The _api virtual directory is mapped to call into client.svc, where the client object model can be used.</span></span>  <br/> |<span data-ttu-id="a8010-122">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-122">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/web/title` <br/> |<span data-ttu-id="a8010-123">Получает название текущего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="a8010-123">Retrieves the title of the current web.</span></span>  <br/> |<span data-ttu-id="a8010-124">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-124">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists` <br/> |<span data-ttu-id="a8010-125">Извлечение всех списков на сайте</span><span class="sxs-lookup"><span data-stu-id="a8010-125">Retrieves all lists on a site.</span></span>  <br/> |<span data-ttu-id="a8010-126">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-126">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')` <br/> |<span data-ttu-id="a8010-127">Извлекает метаданные для указанного списка.</span><span class="sxs-lookup"><span data-stu-id="a8010-127">Retrieves the metadata for a specified list.</span></span>  <br/> |<span data-ttu-id="a8010-128">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-128">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')/items` <br/> |<span data-ttu-id="a8010-129">Извлечение элементов списка в заданном списке.</span><span class="sxs-lookup"><span data-stu-id="a8010-129">Retrieves the list items in a specified list.</span></span>  <br/> |<span data-ttu-id="a8010-130">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-130">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')?select=Title` <br/> |<span data-ttu-id="a8010-131">Извлечение названия определенный список.</span><span class="sxs-lookup"><span data-stu-id="a8010-131">Retrieves the title of a specific list.</span></span>  <br/> |<span data-ttu-id="a8010-132">GET</span><span class="sxs-lookup"><span data-stu-id="a8010-132">GET</span></span>  <br/> |
   

## <a name="constructing-query-strings-for-filtering-data"></a><span data-ttu-id="a8010-133">Создание строки запроса для фильтрации данных</span><span class="sxs-lookup"><span data-stu-id="a8010-133">Constructing query strings for filtering data</span></span>
<span data-ttu-id="a8010-134"><a name="bkmk_constructquery"> </a></span><span class="sxs-lookup"><span data-stu-id="a8010-134"></span></span>

<span data-ttu-id="a8010-135">Чтобы ограничить количество возвращаемых данных или сделать его более относится к пользователю, можно использовать операции фильтрации, найденные в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="a8010-135">In order to limit the amount of data returned, or make it more relevant to the user, you can use the filter operations found in Table 2.</span></span>
  
    
    

<span data-ttu-id="a8010-136">**В таблице 2. Операторы для фильтрации данных**</span><span class="sxs-lookup"><span data-stu-id="a8010-136">**Table 2. Operators for filtering data**</span></span>


|<span data-ttu-id="a8010-137">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="a8010-137">**Operator**</span></span>|<span data-ttu-id="a8010-138">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a8010-138">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a8010-139">eq</span><span class="sxs-lookup"><span data-stu-id="a8010-139">EQ</span></span>  <br/> |<span data-ttu-id="a8010-140">Равняется</span><span class="sxs-lookup"><span data-stu-id="a8010-140">Equals</span></span>  <br/> <span data-ttu-id="a8010-141">**Примечание:** При использовании **EQ** для фильтрации условия фильтра передаются во внешней системе, где происходит фильтрация на сервере.</span><span class="sxs-lookup"><span data-stu-id="a8010-141">**Note:** When you use **EQ** to filter, the filter criteria are passed to the external system where the filtering happens on the server.</span></span>          |
|<span data-ttu-id="a8010-142">Gt</span><span class="sxs-lookup"><span data-stu-id="a8010-142">GT</span></span>  <br/> |<span data-ttu-id="a8010-143">(больше)</span><span class="sxs-lookup"><span data-stu-id="a8010-143">Greater Than</span></span>  <br/> <span data-ttu-id="a8010-144">**Примечание:** При использовании оператора **GT** выполняется фильтрация только со стороны клиента. > Например: `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` возвращает все заголовки со средним рейтинг более чем 3.</span><span class="sxs-lookup"><span data-stu-id="a8010-144">**Note:** When you use the **GT** operator, only client-side filtering is executed.> For example:  `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` returns all titles with an average rating over 3.</span></span>          |
   

> <span data-ttu-id="a8010-145">**Примечание:** Для получения столбцов, которые являются частью связь, необходимо явно включить столбец в URL-адрес, с помощью **$select** в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="a8010-145">**Note:** To retrieve columns that are part of an association, you must explicitly include the column in the URL using **$select** in the query string.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="a8010-146">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8010-146">Additional resources</span></span>
<span data-ttu-id="a8010-147"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a8010-147"></span></span>


-  [<span data-ttu-id="a8010-148">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-148">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a8010-149">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="a8010-149">Complete basic operations using SharePoint REST endpoints</span></span>](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="a8010-150">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-150">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="a8010-151">SharePoint: выполнение основных операций доступа к данным в приложениях с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a8010-151">SharePoint: Perform basic data access operations by using REST in apps</span></span>](http://code.msdn.microsoft.com/SharePoint-Perform-335d925b)
    
  
-  [<span data-ttu-id="a8010-152">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-152">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a8010-153">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8010-153">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
