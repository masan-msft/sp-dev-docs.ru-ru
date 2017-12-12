---
title: "Создание поисковых запросов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c4372fcc-4574-4c81-a345-a1bb282ca8f7
ms.openlocfilehash: d2dfcbbe782057d012f72ca05328316638db635f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="building-search-queries-in-sharepoint"></a>Создание поисковых запросов в SharePoint
Узнайте о синтаксисе поиска, который поддерживается в SharePoint для создания правил запроса и поисковых запросов.
## <a name="supported-search-syntax-in-sharepoint-for-building-search-queries"></a>Поддерживаемый синтаксис поиска в SharePoint для создания поисковых запросов
<a name="SP15Buildquery_support"> </a>

Поиск в SharePoint поддерживает синтаксис языка запросов по ключевым словам (KQL) и языка запросов FAST (FQL).
  
    
    
 **Язык запросов по ключевым словам (KQL)**
  
    
    
KQL  это язык запросов для создания поисковых запросов, использующийся по умолчанию. С его помощью можно задать условия поиска или ограничения свойств, передающиеся в службу поиска SharePoint.
  
    
    
 **Язык запросов FAST (FQL)**
  
    
    
FQL  это язык SQL, поддерживающий расширенные операторы запросов. Его можно использовать для создания сложных запросов, которые необходимо программно передать в службу запросов SharePoint. FQL не предназначен для пользователей и отключен по умолчанию. 
  
    
    
Чтобы его включить, используйте свойство **EnableFQL**. Затем скопируйте источник результатов по умолчанию и измените строку преобразования запроса  `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}` на одном из трех уровней (в приложении службы поиска, или SSA, семействе веб-сайтов, а также на сайте), одним из этих способов:
  
    
    

- Удалите фильтр KQL  `-ContentClass:urn:content-class:SPSPeople` в строке преобразования запроса. В результате получится следующая строка: `{?{searchTerms}}`.
    
  
- Замените строку преобразования запроса на эквивалентную строку на языке FQL, например `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.
    
  
Дополнительные сведения об источниках результатов и принципах их использования см. в статьях [Источники результатов](http://office.microsoft.com/ru-RU/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) и [Настройка источников результатов для поиска в SharePoint](http://technet.microsoft.com/ru-RU/library/jj683115%28v=office.15%29.aspx).
  
    
    

## <a name="in-this-section"></a>В этом разделе:
<a name="SP15Buildquery_support"> </a>


-  [Справочник по синтаксису языка запросов по ключевым словам (KQL)](keyword-query-language-kql-syntax-reference.md)
    
  
-  [справочник по синтаксису языка запросов FAST (FQL)](fast-query-language-fql-syntax-reference.md)
    
  
-  [Использование API поисковых запросов SharePoint](using-the-sharepoint-search-query-apis.md)
    
  

## <a name="see-also"></a>См. также
<a name="SP15Buildquery_addlresources"> </a>


-  [Поиск в SharePoint](search-in-sharepoint.md)
    
  
-  [Планирование преобразования запросов и упорядочивания результатов в SharePoint](http://technet.microsoft.com/ru-RU/library/jj219620%28v=office.15%29.aspx)
    
  
-  [Переменные запроса в SharePoint](http://technet.microsoft.com/ru-RU/library/jj683123.aspx)
    
  

