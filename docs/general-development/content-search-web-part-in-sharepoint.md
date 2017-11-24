---
title: "Веб-часть поиска контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6fb4bf41-0846-4dca-ad9e-906afdfd3d2b
ms.openlocfilehash: 9585738005f8fb2ed7581ef8245b60c60c16ff5b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="content-search-web-part-in-sharepoint"></a>Веб-часть поиска контента в SharePoint

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
Сведения о веб-части поиска контента (CSWP) в SharePoint.
## <a name="introducing-the-content-search-web-part-cswp"></a>Краткие сведения о веб-части поиска контента (CSWP)
<a name="SP15_CSWP_IntroducingCSWP"> </a>

Веб часть содержимого поиска (CSWP) — это веб-части, введенные в SharePoint, которое использует различные параметры стилей для отображения динамического содержимого на страницах SharePoint.
  
    
    

## <a name="how-the-content-search-web-part-works"></a>Как работает веб-части поиска контента
<a name="SP15_CSWP_HowCSWPWorks"> </a>

Веб-часть контента поиска отображает результаты поиска, чтобы легко можно отформатировать. Каждый контента веб-части поиска связан с поискового запроса и показаны результаты для данного запроса поиска.
  
    
    
Изменение отображения результатов на странице можно использовать шаблоны для отображения. Шаблоны отображения, фрагментов кода HTML и JavaScript, которые отображают сведения, возвращаемые SharePoint. Сведения для отображения получает вставлено на страницу в формате JSON. 
  
    
    

## <a name="when-to-use-the-content-search-web-part-cswp-or-the-content-query-web-part-cqwp"></a>Когда следует использовать часть содержимого Web поиска (CSWP) или часть содержимого Web запросов (CQWP)
<a name="SP15_CSWP_WhenToUseCSWPorCQWP"> </a>

CSWP может вернуть любое содержимое из индекса поиска. Применяется для сайтов SharePoint, если подключение к службе поиска, чтобы вернуться на страницах результатов индексированного поиска. 
  
    
    
CSWP возвращает содержимое, максимально актуальными последнего обхода контента, поэтому если часто обхода контента, контент, который возвращает CSWP более современные, чем при обходом редко. Если необходимо отображать мгновенные содержимого или обновленную версию содержимого, используйте части Web содержимое запроса (CQWP).
  
    
    
Поиска обходит только основных версий содержимого, никогда не вспомогательных версий. Если необходимо отобразить вспомогательных версий содержимого, сделайте это с помощью CQWP.
  
    
    
Некоторые администраторы семейства сайтов пометить как сайты, чтобы не будет индексироваться. Содержимое, помеченные таким образом не доступны в CSWP. Если вы хотите возвращать результаты с сайта, который помечается не индекса, используйте CQWP.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_CSWP_AdditionalResources"> </a>


-  [Управляемой навигации в SharePoint](managed-navigation-in-sharepoint.md)
    
  
-  [Новые возможности поиска в SharePoint для разработчиков (en)](what-s-new-in-sharepoint-search-for-developers.md)
    
  
