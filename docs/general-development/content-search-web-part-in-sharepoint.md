---
title: "Веб-часть \"Поиск контента\" в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6fb4bf41-0846-4dca-ad9e-906afdfd3d2b
ms.openlocfilehash: 127e71765887f369191f1d468485eca916162f48
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="content-search-web-part-in-sharepoint"></a><span data-ttu-id="fffa6-102">Веб-часть "Поиск контента" в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fffa6-102">Content Search Web Part in SharePoint</span></span>

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="fffa6-104">Сведения о веб-части поиска контента (CSWP) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fffa6-104">Learn about the Content Search Web Part (CSWP) in SharePoint.</span></span>
## <a name="introducing-the-content-search-web-part-cswp"></a><span data-ttu-id="fffa6-105">Краткие сведения о веб-части поиска контента (CSWP)</span><span class="sxs-lookup"><span data-stu-id="fffa6-105">Introducing the Content Search Web Part (CSWP)</span></span>
<span data-ttu-id="fffa6-106"><a name="SP15_CSWP_IntroducingCSWP"> </a></span><span class="sxs-lookup"><span data-stu-id="fffa6-106"></span></span>

<span data-ttu-id="fffa6-107">Веб часть содержимого поиска (CSWP) — это веб-части, введенные в SharePoint, которое использует различные параметры стилей для отображения динамического содержимого на страницах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fffa6-107">The Content Search Web Part (CSWP) is a Web Part introduced in SharePoint that uses various styling options to display dynamic content on SharePoint pages.</span></span>
  
    
    

## <a name="how-the-content-search-web-part-works"></a><span data-ttu-id="fffa6-108">Как работает веб-части поиска контента</span><span class="sxs-lookup"><span data-stu-id="fffa6-108">How the Content Search Web Part works</span></span>
<span data-ttu-id="fffa6-109"><a name="SP15_CSWP_HowCSWPWorks"> </a></span><span class="sxs-lookup"><span data-stu-id="fffa6-109"></span></span>

<span data-ttu-id="fffa6-p101">Веб-часть контента поиска отображает результаты поиска, чтобы легко можно отформатировать. Каждый контента веб-части поиска связан с поискового запроса и показаны результаты для данного запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="fffa6-p101">Content Search Web Part displays search results in a way that you can easily format. Each Content Search Web Part is associated with a search query and shows the results for that search query.</span></span>
  
    
    
<span data-ttu-id="fffa6-p102">Изменение отображения результатов на странице можно использовать шаблоны для отображения. Шаблоны отображения, фрагментов кода HTML и JavaScript, которые отображают сведения, возвращаемые SharePoint. Сведения для отображения получает вставлено на страницу в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="fffa6-p102">You can use display templates to change how search results appear on the page. Display templates are snippets of HTML and JavaScript that render the information returned by SharePoint. The information to be displayed gets inserted into the page in JSON format.</span></span> 
  
    
    

## <a name="when-to-use-the-content-search-web-part-cswp-or-the-content-query-web-part-cqwp"></a><span data-ttu-id="fffa6-115">Когда следует использовать часть содержимого Web поиска (CSWP) или часть содержимого Web запросов (CQWP)</span><span class="sxs-lookup"><span data-stu-id="fffa6-115">When to use the Content Search Web Part (CSWP) or the Content Query Web Part (CQWP)</span></span>
<span data-ttu-id="fffa6-116"><a name="SP15_CSWP_WhenToUseCSWPorCQWP"> </a></span><span class="sxs-lookup"><span data-stu-id="fffa6-116"></span></span>

<span data-ttu-id="fffa6-117">CSWP может вернуть любое содержимое из индекса поиска.</span><span class="sxs-lookup"><span data-stu-id="fffa6-117">The CSWP can return any content from the search index.</span></span> <span data-ttu-id="fffa6-118">Применяется для сайтов SharePoint, если подключение к службе поиска, чтобы вернуться на страницах результатов индексированного поиска.</span><span class="sxs-lookup"><span data-stu-id="fffa6-118">Use it on your SharePoint sites when you are connecting to a search service and want to return indexed search results in your pages.</span></span> 
  
    
    
<span data-ttu-id="fffa6-p104">CSWP возвращает содержимое, максимально актуальными последнего обхода контента, поэтому если часто обхода контента, контент, который возвращает CSWP более современные, чем при обходом редко. Если необходимо отображать мгновенные содержимого или обновленную версию содержимого, используйте части Web содержимое запроса (CQWP).</span><span class="sxs-lookup"><span data-stu-id="fffa6-p104">The CSWP returns content that is as fresh as the latest crawl of your content, so if you crawl often, the content that the CSWP returns is more up-to-date than if you crawl infrequently. If you need to display instant content or the refreshed version of content, use the Content Query Web Part (CQWP) instead.</span></span>
  
    
    
<span data-ttu-id="fffa6-p105">Поиска обходит только основных версий содержимого, никогда не вспомогательных версий. Если необходимо отобразить вспомогательных версий содержимого, сделайте это с помощью CQWP.</span><span class="sxs-lookup"><span data-stu-id="fffa6-p105">Search crawls only the major versions of content, never the minor versions. If you want to display the minor versions of your content, do that by using a CQWP.</span></span>
  
    
    
<span data-ttu-id="fffa6-p106">Некоторые администраторы семейства сайтов пометить как сайты, чтобы не будет индексироваться. Содержимое, помеченные таким образом не доступны в CSWP. Если вы хотите возвращать результаты с сайта, который помечается не индекса, используйте CQWP.</span><span class="sxs-lookup"><span data-stu-id="fffa6-p106">Some site collection administrators mark sites to not be indexed. Content marked in this way is not available in a CSWP. If you want to return results from a site that is marked to not index, use the CQWP instead.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="fffa6-126">См. также</span><span class="sxs-lookup"><span data-stu-id="fffa6-126">See also</span></span>
<span data-ttu-id="fffa6-127"><a name="SP15_CSWP_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="fffa6-127"></span></span>


-  [<span data-ttu-id="fffa6-128">Управляемой навигации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fffa6-128">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="fffa6-129">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="fffa6-129">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

