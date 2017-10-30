---
title: "Настройка службы поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e447127c-2b11-4d65-b46e-01a18cdcdee5
ms.openlocfilehash: 0fa1ba925fd858ebef033a89bf98f0fe566fb167
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="configure-search-in-sharepoint"></a><span data-ttu-id="83b2b-102">Настройка службы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b2b-102">Configure search in SharePoint</span></span>
<span data-ttu-id="83b2b-103">Узнайте о двух типах настройки в поиска SharePoint: Добавление настраиваемого разбиения и Добавление настраиваемого шага для изменения управляемых свойств для обхода элементов во время обработки контента.</span><span class="sxs-lookup"><span data-stu-id="83b2b-103">Learn about the two types of customization in SharePoint search: adding a custom word breaker and adding a custom step to modify managed properties for crawled items during content processing.</span></span>
   

## <a name="adding-a-custom-word-breaker-in-sharepoint"></a><span data-ttu-id="83b2b-104">Добавление настраиваемого разбиения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b2b-104">Adding a custom word breaker in SharePoint</span></span>
<span data-ttu-id="83b2b-105"><a name="SP15configsearch_word"> </a></span><span class="sxs-lookup"><span data-stu-id="83b2b-105"></span></span>

<span data-ttu-id="83b2b-p101">Настраиваемые разбиения можно добавить для настройки word нарушение поведение в соответствии со своими потребностями. Настраиваемые разбиения можно использовать для замены существующей средства разбиения по словам на том же языке. Кроме того можно использовать настраиваемого разбиения для замены существующей средства разбиения по словам, другой язык.</span><span class="sxs-lookup"><span data-stu-id="83b2b-p101">A custom word breaker can be added to tune word breaking behavior according to your needs. You can use a custom word breaker to replace the existing word breaker of the same language. Alternately, you can use a custom word breaker to replace the existing word breaker with that of a different language.</span></span>
  
    
    

## <a name="adding-a-custom-step-to-modify-managed-properties-in-sharepoint"></a><span data-ttu-id="83b2b-109">Добавление настраиваемого шага для изменения управляемых свойств в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b2b-109">Adding a custom step to modify managed properties in SharePoint</span></span>
<span data-ttu-id="83b2b-110"><a name="SP15ConfigSearch_customstep"> </a></span><span class="sxs-lookup"><span data-stu-id="83b2b-110"></span></span>

<span data-ttu-id="83b2b-p102">Изменение управляемого свойства в виде внешнего повышения качества контента веб-службы можно добавить настраиваемого шага. Повышения качества контента веб-службы  это служба, можно создать для получения выноски от клиента веб-службы в компонент обработки контента. Настраиваемая полезных данных, затем отправить веб-службы и ответа объединяется для обхода элементов перед добавлением в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="83b2b-p102">A custom step can be added to modify managed properties in the form of an external content enrichment web service. The content enrichment web service is a service that you can create to receive a callout from the web service client inside the content processing component. A configurable payload is then submitted to the web service, and the response is merged into the crawled item before it is added to the search index.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="83b2b-114">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="83b2b-114">In this section</span></span>
<span data-ttu-id="83b2b-115"><a name="SP15ConfigSearch_customstep"> </a></span><span class="sxs-lookup"><span data-stu-id="83b2b-115"></span></span>


-  [<span data-ttu-id="83b2b-116">Настраиваемые средства разбиения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b2b-116">Custom word breakers in SharePoint</span></span>](custom-word-breakers-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="83b2b-117">Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"</span><span class="sxs-lookup"><span data-stu-id="83b2b-117">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="83b2b-118">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="83b2b-118">Additional resources</span></span>
<span data-ttu-id="83b2b-119"><a name="SP15configsearch_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="83b2b-119"></span></span>


-  [<span data-ttu-id="83b2b-120">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b2b-120">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="83b2b-121">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="83b2b-121">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

