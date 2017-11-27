---
title: "Создание на основе механизмов поиска мобильных приложений с помощью интерфейсов навигации и REST ведение журнала событий"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5b313130-500c-4ccf-80ea-b102f30e5afb
ms.openlocfilehash: 98ba8acf95b52ddc183574684901923b4544e37c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="build-search-driven-mobile-apps-with-the-navigation-and-event-logging-rest-interfaces"></a>Создание на основе механизмов поиска мобильных приложений с помощью интерфейсов навигации и REST ведение журнала событий

SharePoint представляется интерфейсы навигации и REST ведение журнала событий, позволяя создавать мобильного приложения для мобильных устройств, например телефонов и планшетные ПК под управлением операционных системах, отличных от Windows, управляемых с помощью поиска — например, Android и операций ввода-вывода.
## <a name="how-apps-work-with-the-product-catalog"></a>Как работают приложения с каталогом продуктов
<a name="mobile_app_and_product_catalog"> </a>

Каталог продуктов могут отображаться на мобильном устройстве различными способами. В большинстве случаев можно настроить канала мобильного устройства для каталога продуктов в среде SharePoint. Создание канала мобильного устройства можно настраивать внешний вид и функции, которая соответствует любого размера экрана на мобильном устройстве. Страница с результатами отображаются в. Формат ASPX, с помощью веб-браузера на мобильном устройстве. Структура страниц и его соответствующей логики обрабатывается на сервере под управлением SharePoint. С другой стороны созданных с помощью интерфейсов навигации и REST ведение журнала событий приложения на основе механизмов поиска и действует как сервер переднего плана перейдите структуры каталога продуктов.
  
    
    
Приложение не является отдельной программы, но работает с каталогом продуктов заданы в существующую установку SharePoint. Приложения могут динамическое обновление структуры переходов, если каталог продуктов был изменен в установленных SharePoint. Кроме того, установите переключатель в положение события, сделанные пользователем отправляются на сервере под управлением SharePoint для повышения общего качества рекомендации, сделанных с каталога продуктов.
  
    
    
Приложение создает страниц, которые необходимы пользователю для просмотра каталог продуктов без использования веб-браузера. Главные страницы, макеты страниц и логику для создания страниц, чтобы просмотреть каталог продуктов загружаются на устройствах приложения; Эти страницы используются повторно, каждый раз, когда пользователь запускает приложение. При переходе каталог продуктов приложения одновременно создает структуру переходов и настраивает страницы. Чтобы заполнить соответствующие страницы с содержимым элемента, поисковых запросов, передаются в каталог продуктов в SharePoint. Соответствующие результаты поиска затем используется для заполнения страницы.
  
    
    

## <a name="example-create-a-search-driven-mobile-app-with-home-category-and-item-detail-pages"></a>Пример: Создание мобильного приложения на основе механизмов поиска с домашней, категории, а элемент страницы сведений о
<a name="example_search_driven_mobile_app"> </a>

Предположим, что у вас есть мобильного приложения с использованием трех типов страниц: домашней страницы, страницы категорий и страницы сведений о элемента. В следующих разделах, как использовать интерфейсы навигации, ведение журнала событий и поиска REST для создания страниц.
  
    
    

### <a name="home-page-for-a-search-driven-mobile-app"></a>Домашняя страница для мобильного приложения на основе поиска

Обычно на **домашней** странице отображается при запуске приложения. На **домашней** странице содержит меню каталога продукции, какой-либо текст и Неподвижное изображение, как показано на рисунке 1.
  
    
    

**На рисунке 1. Домашняя страница для мобильного приложения на основе поиска**

  
    
    

  
    
    
![Создание мобильных приложений на основе поиска](../images/SP15_Buildsearch-drivenmobileappspages_home.gif)
  
    
    
Для создания на этой странице, приложение отправляет навигации REST-вызов на сервер под управлением SharePoint запрашивает структуры переходов каталога продуктов. Затем приложение использует данные ответа для установки правильных таксономии или структуре меню и отображает имена правильный терминов для каталога продуктов. Дополнительное содержимое, такие как макет страницы, текст заголовка и статические изображения хранятся в самом приложении. При изменении таксономии в дальнейшем приложения могут обновиться REST навигации вызова при выполнении.
  
    
    
Ниже приведен пример типичного вызовов REST навигации.
  
    
    



```

GET http://server/_api/navigation/menustate?mapprovidername='GlobalNavigationSwitchableProvider'

```

Показано соответствующего ответа в  [Пример ответа для навигации REST вызываться для мобильного приложения](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md#response_navigation_rest).
  
    
    

### <a name="category-page-for-a-search-driven-mobile-app"></a>Страница категорий для мобильного приложения на основе поиска

На странице **категорий** отображается много элементов в выбранной категории. Обычно каждого элемента в категории могут быть представлены некоторые данные соответствующего элемента, такие как заголовок, изображения и цену. Эти данные собираются из каталога продуктов с помощью запроса поиска в службе REST поиска SharePoint, как показано на рисунке 2.
  
    
    

**На рисунке 2. Страница категорий для мобильного приложения на основе поиска**

  
    
    

  
    
    
![Создание мобильных приложений на основе поиска](../images/Buildsearch-drivenmobileappspages.gif)
  
    
    
При выборе одной из категорий на предыдущем рисунке, к примеру, **TV** страницы **категорий** отображается.
  
    
    
Ниже приведен пример типичного запроса поиска REST для получения содержимого для определенной категории.
  
    
    



```

GET http://server/_api/search/query?querytext='owstaxidProductCatalogItemCategory:#0<TermGuid>'

```

В  [Пример ответа на запрос поиска REST для мобильного приложения](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md#response_search_rest)отображается соответствующего ответа.
  
    
    
Компонент в SharePoint обработки запросов возвращает результаты поиска, которые содержат данные для определенной категории, и приложение отображает данные на странице " **категории** ". Если наиболее подходящего элемента, связанного с выбранной категории, компонент обработки запросов обнаруживает этого сопоставления и извлекает данные наиболее подходящий элемент из базы данных наиболее подходящего элемента, с меткой **BB** на схеме. Результаты поиска нажмите mixed с результатами из базы данных наиболее подходящий элемент и отправляются обратно в приложение в таблице результатов. Приложение отвечает за извлечение различных частей результатов из таблицы и отображение наиболее подходящего элемента в выделенной папке.
  
    
    

### <a name="item-detail-pages-for-a-search-driven-mobile-app"></a>Страницы сведений о элемента для мобильного приложения на основе поиска

При выборе элемента в категории, откроется страница **сведений об элементе**. На этой странице элемент подробно с данными, такие как заголовок, изображения продуктов, технические описания, цены и сведения о доставке. Дополнительные рекомендации по или оценки, если он доступен, также отображаются. Для создания страницы **сведений об элементе**, приложение отправляет два запроса: один запрос для получения данных элемента, а второй запрос на получение рекомендации связанные с этого элемента, как показано на рисунке 3.
  
    
    

**На рисунке 3. Страница сведений об элементах для мобильного приложения на основе поиска**

  
    
    

  
    
    
![Создание приложения на основе поиска](../images/Buildsearch-drivenmobileappspages_item_details.gif)
  
    
    
Ниже приведен пример типичного запроса поиска REST для получения содержимого для определенного элемента.
  
    
    



```

GET http://server/_api/search/query?querytext='ProductCatalogItemNumberOWSTEXT:1234567'
```

Рекомендации по вычисляются в SharePoint, не в самом приложении. Для создания рекомендации, основанные на события пользователя  не только в этот определенного приложения, но все события пользователя, собранные по каталогу продукции  приложение постоянно отправляет события пользователя, когда они возникают, обратно в каталог продуктов в SharePoint с помощью вызова события. Эти события пользователя хранятся в журнале событий и обрабатываются только как другой пользователь событий, связанных с элемента. Обратный вызов не отправляется приложения из каталога продуктов. Рекомендации по вычисляется доступны для приложения в службе REST поиска SharePoint.
  
    
    
Пример типичного **POST** звонка для ведения журнала событий.
  
    
    



```
POST http://server/_api/events/logevent
{
      "usageEntry": {
            "__metadata": {
                  "type": "Microsoft.SharePoint.Administration.UsageEntry"
            },
            "EventTypeId": 1,
            "ItemId": "an item fb7c-4196-8123-e54eee5f4787",
            "ScopeId": "61141c0e-fb7c ",
            "Site": "61141c0e- 
-4196-8123-e54eee5f4787",
            "User": "johndoe"
      }
}
```

Служба исходя из стандартных кодов возврата HTTP: ответ HTTP 200 указывает успешный запрос. Нет ответов из каталога продуктов для интерфейса REST ведения журнала событий.
  
    
    

## <a name="example-response-for-a-navigation-rest-call-for-a-mobile-app"></a>Пример ответа для навигации REST вызываться для мобильного приложения
<a name="response_navigation_rest"> </a>


```

<?xml version="1.0" encoding="utf-8"?>
<d:MenuState xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:type="SP.MenuState">

  <d:FriendlyUrlPrefix>/sites/contoso/</d:FriendlyUrlPrefix>
  <d:Nodes>
    <d:element m:type="SP.MenuNode">
      <d:CustomProperties m:null="true" />
      <d:FriendlyUrlSegment>electronics</d:FriendlyUrlSegment>
      <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
      <d:Key>16c4c3c8-0309-47f7-9d9b-17e699febce8</d:Key>
      <d:Nodes>
        <d:element m:type="SP.MenuNode">
          <d:CustomProperties m:null="true" />
          <d:FriendlyUrlSegment>audio</d:FriendlyUrlSegment>
          <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
          <d:Key>3e2d5c67-3fad-4cfa-8e1c-8c74fdf3a34b</d:Key>
          <d:Nodes>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>car-audio</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>e3d271a4-dcbf-464d-a557-23848ccaa54f</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Car audio</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>headphones</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>7ad146d0-61b5-4b55-9da0-db7eaaa20f4a</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Headphones</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>mp3</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>7387fe97-52fa-464b-878a-b05d04e7032e</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>MP3</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>speakers</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>65da907c-9565-45f6-a278-cbce7f74ab3d</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Speakers</d:Title>
            </d:element>
          </d:Nodes>
          <d:NodeType m:type="Edm.Int32">1</d:NodeType>
          <d:SimpleUrl></d:SimpleUrl>
          <d:Title>Audio</d:Title>
        </d:element>
      </d:Nodes>
      <d:NodeType m:type="Edm.Int32">1</d:NodeType>
      <d:SimpleUrl></d:SimpleUrl>
      <d:Title>Electronics</d:Title>
    </d:element>
  </d:Nodes>
  <d:SimpleUrl m:null="true" />
  <d:SPSitePrefix>/sites/contoso/</d:SPSitePrefix>
  <d:SPWebPrefix>/sites/contoso/</d:SPWebPrefix>
  <d:StartingNodeKey>2168423f-3fea-4324-a5cb-90be8f079750</d:StartingNodeKey>
  <d:StartingNodeTitle>contoso</d:StartingNodeTitle>
  <d:Version>2012-05-29T12:00:04.4747484Z</d:Version>
</d:MenuState>

```


## <a name="example-response-for-a-search-rest-query-for-a-mobile-app"></a>Пример ответа на запрос поиска REST для мобильного приложения
<a name="response_search_rest"> </a>


```

<d:query xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:type="Microsoft.Office.Server.Search.REST.SearchResult">
  <d:ElapsedTime m:type="Edm.Int32">4640</d:ElapsedTime>
  <d:PrimaryQueryResult m:type="Microsoft.Office.Server.Search.REST.QueryResult">
    <d:CustomResults m:null="true"/>
    <d:QueryId>7fea4ced-5789-4067-beab-8f807410b29e</d:QueryId>
    <d:QueryRuleId m:type="Edm.Guid">00000000-0000-0000-0000-000000000000</d:QueryRuleId>
    <d:RefinementResults m:null="true"/>
    <d:RelevantResults m:type="Microsoft.Office.Server.Search.REST.RelevantResults">
      <d:GroupTemplateId m:null="true"/>
      <d:ItemTemplateId m:null="true"/>
      <d:Properties>
        ...
      </d:Properties>
      <d:ResultTitle m:null="true"/>
      <d:ResultTitleUrl m:null="true"/>
      <d:RowCount m:type="Edm.Int32">10</d:RowCount>
      <d:Table m:type="SP.SimpleDataTable">
        <d:Rows>
          ...
        </d:Rows>
      </d:Table>
      <d:TotalRows m:type="Edm.Int32">2048964</d:TotalRows>
      <d:TotalRowsIncludingDuplicates m:type="Edm.Int32">2048964</d:TotalRowsIncludingDuplicates>
    </d:RelevantResults>
    <d:SpecialTermResults m:null="true"/>
  </d:PrimaryQueryResult>
  <d:Properties>
    ...
  </d:Properties>
  <d:SecondaryQueryResults m:null="true"/>
  <d:SpellingSuggestion/>
  <d:TriggeredRules>
  </d:TriggeredRules>
</d:query>
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Программирование с использованием службы SharePoint 2013 REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

