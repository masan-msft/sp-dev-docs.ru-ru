---
title: "Получение предложений запроса, с помощью службы Search REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a64c5bec-64a8-4752-9c72-433d1c864aed
ms.openlocfilehash: 64f07696df6df14756303a53dd75f41de9ccbdbf
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="retrieving-query-suggestions-using-the-search-rest-service"></a>Получение предложений запроса, с помощью службы Search REST
Узнайте, как использовать службы поиска REST из клиентов и мобильных приложений для извлечения предложений запроса из поиска в SharePoint.
Предложения запроса, также известной как предложения поиска, фраз, которые пользователи уже выполнен поиск и, или отобразить «предложенные» им как люди вводят свои запросы. Чтобы включить предложения запроса до и после запроса можно использовать поиска в SharePoint. Эти варианты отображаются в списке под окном поиска, как пользователь вводит запрос. Дополнительные сведения о предложений запроса, а также для включения их можно [Управление предложениями запроса в SharePoint](http://technet.microsoft.com/en-us/library/jj721441.aspx).
  
    
    


## <a name="suggest-endpoint-in-the-search-rest-service"></a>Предложить конечной точки в службе REST поиска
<a name="bk_SuggestEndpoint"> </a>

Службы REST поиска включает в себя **Suggest** конечной точки, которые можно использовать в любой технологии, поддерживающей веб-запросы REST для получения предложений запроса, поисковая система генерирует для запросов от клиента или приложения для мобильных устройств.
  
    
    
URI для **GET** запросов к конечной точке службы поиска REST **Suggest**  это:
  
    
    
 `/_api/search/suggest`
  
    
    
В URL-адрес заданы параметры предложения запроса. Можно создать URL-адрес запроса двумя способами:
  
    
    


  
    
    
>  `http://server/_api/search/suggest?parameter=value&amp;parameter=value`
    
  

  
    
    
>  `http://server/_api/search/suggest(parameter=value&amp;parameter=value)`
    
  
> [!NOTE]
> [!Примечание] Службы поиска REST не поддерживает анонимные запросы к конечной точке **Suggest**.
  
    
    


## <a name="query-suggestion-parameters"></a>Параметры предложений запроса
<a name="bk_SuggestParameters"> </a>

В следующих разделах описываются параметры, которые можно использовать для конечной точки **Suggest**.
  
    
    

### <a name="querytext"></a>Текст запроса

Строка, содержащая текст для запроса поиска.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint"
  
    
    

### <a name="inumberofquerysuggestions"></a>iNumberOfQuerySuggestions

Количество предложений запроса для извлечения. Должен быть больше нуля (0). Значение по умолчанию  5.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; inumberofquerysuggestions = 3
  
    
    

### <a name="inumberofresultsuggestions"></a>iNumberOfResultSuggestions

Число личных результаты для извлечения. Должен быть больше нуля (0). Значение по умолчанию  5.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; inumberofresultsuggestions = 4
  
    
    

### <a name="fprequerysuggestions"></a>fPreQuerySuggestions

Логическое значение, указывающее, следует ли извлекать предложения запроса до или после запроса. **true** для возврата предложения перед запроса; в противном случае  **false**. Значение по умолчанию  **false**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fprequerysuggestions = true
  
    
    

### <a name="fhithighlighting"></a>fHitHighlighting

Логическое значение, которое указывает, следует ли для сбора данных для выделения и форматирования полужирным шрифтом предложений запроса. **true** форматирование полужирным шрифтом условия предложений возвращенные запроса, которые соответствуют терминов в указанного запроса; в противном случае  **false**. Значение по умолчанию  **true**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fhithighlighting = false
  
    
    

### <a name="fcapitalizefirstletters"></a>fCapitalizeFirstLetters

Логическое значение, которое указывает, следует ли преобразование первой буквы в каждого термина в предложения возвращенные запроса. **true** прописной первую букву в каждом терминов; в противном случае  **false**. Значение по умолчанию  **false**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fcapitalizefirstletters = false
  
    
    

### <a name="culture"></a>Culture

Код языка (LCID) для запроса (см. статью  [Коды языков, присвоенные Майкрософт](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; EventID = 1044
  
    
    

### <a name="enablestemming"></a>EnableStemming

Логическое значение, указывающее, включено ли выделение корней. **true**, чтобы включить извлечение корней слов; в противном случае  **false**. Значение по умолчанию  **true**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; enablestemming = false
  
    
    

### <a name="showpeoplenamesuggestions"></a>ShowPeopleNameSuggestions

Логическое значение, указывающее, следует ли включать имена людей в предложения возвращенные запроса. **true** для включения имен людей в предложения возвращенные запроса; в противном случае  **false**. Значение по умолчанию  **true**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; showpeoplenamesuggestions = false
  
    
    

### <a name="enablequeryrules"></a>EnableQueryRules

Логическое значение, которое указывает, следует ли включить правила запросов для этого запроса. **true** Включение правила запросов; в противном случае  **false**. Значение по умолчанию  **true**.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; enablequeryrules = false
  
    
    

### <a name="fprefixmatchallterms"></a>fPrefixMatchAllTerms

Сопоставляет значение Boolean, указывающее, нужно ли возвращать предложения запроса для префикса. **true** для возврата на основе префикса предложений запроса соответствует, в противном случае **false** при предложений запроса должна соответствовать word полного запроса.
  
    
    
 **Пример запроса GET**
  
    
    
http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fprefixmatchallterms = false
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Общие сведения об API службы поиска REST для SharePoint](sharepoint-search-rest-api-overview.md)
    
  
-  [Поиск в SharePoint](search-in-sharepoint.md)
    
  
-  [SharePoint: использование службы поиска REST в приложении для SharePoint](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  
-  [Новые возможности поиска в SharePoint для разработчиков (en)](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [Программирование с использованием службы SharePoint 2013 REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

  
    
    

