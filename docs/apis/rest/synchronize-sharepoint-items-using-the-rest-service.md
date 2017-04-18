# <a name="synchronize-sharepoint-items-using-the-rest-service"></a>Синхронизация элементов SharePoint с помощью службы REST
Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса **GetListItemChangesSinceToken**, входящего в состав службы REST в SharePoint.

## <a name="synchronizing-sharepoint-items-using-the-getlistitemchangessincetoken-resource"></a>Синхронизация элементов SharePoint с помощью ресурса GetListItemChangesSinceToken
Синхронизировать элементы между SharePoint и надстройками или службами можно с помощью ресурса **GetListItemChangesSinceToken**. **GetListItemChangesSinceToken** — это элемент службы SharePoint REST, соответствующий вызову веб-службы **Lists.GetListItemChangesSinceToken**.
 
Выполните запрос **POST**, который содержит в тексте объект [Свойства объекта SP.ChangeLogItemQuery](#bk_props).
 
Запрос вернет XML-файл с **набором строк** ADO, которые соответствуют любым изменениям элементов списка, соответствующим указанному запросу. Дополнительные сведения об этих свойствах, в том числе структуры данных свойств, описание элементов CAML и возвращаемые значения, см. в разделе **Lists.GetListItemChangesSinceToken**.
 
||
|:-----|
|**Пример запроса**|
| `POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`|
|**Пример текста запроса POST**|
|
```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '<Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>',
    'QueryOptions': '<QueryOptions>
      <IncludeMandatoryColumns>FALSE</IncludeMandatoryColumns>
      <DateInUtc>False</DateInUtc>
      <IncludePermissions>TRUE</IncludePermissions>
      <IncludeAttachmentUrls>FALSE</IncludeAttachmentUrls>
      <Folder>Shared Documents/Test1</Folder></QueryOptions>', 
    'ChangeToken':'1;3;eee4c6d5-f88a-42c4-8ce1-685122984870;634397182229400000;3710', 
    'Contains':'<Contains>
      <FieldRef Name="Title"/>
      <Value Type="Text">Testing</Value></Contains>' } 
  } 
}

```

|

## <a name="spchangelogitemquery-object-properties"></a>Свойства объекта SP.ChangeLogItemQuery
<a name="bk_props"> </a>
****

|**Свойство**|**Описание**|
|:-----|:-----|
|**ListName**|Строка, которая содержит название или GUID для списка. При запросе таблицы UserInfo строка содержит UserInfo. Использование GUID приводит к повышению производительности.|
|**ViewName**|Строка, содержащая GUID представления, которое необходимо использовать для атрибутов по умолчанию, представленных параметрами _Query_, _viewFields_ и _rowLimit_. Если этот аргумент не указан, используется представление по умолчанию. Если указано, значение параметра _Query_, _viewFields_ или _rowLimit_ переопределяет соответствующее значение в представлении. Например, если в представлении, заданном с помощью параметра _viewFields_, установлено ограничение на количество строк 100, но параметр _rowLimit_ содержит значение 1000, то в ответе будет 1000 строк.|
|**Query**|Элемент [Query](http://msdn.microsoft.com/en-us/library/ms471093.aspx), содержащий запрос, который определяет, какие записи возвращаются и в каком порядке.|
|**QueryOptions**|Фрагмент XML следующей формы, содержащий отдельные узлы для различных свойств объекта **SPQuery**.|
|**ChangeToken**|Строка, содержащая токен изменений для запроса. Описание формата этой строки см. в статье [Обзор журнала изменений](http://msdn.microsoft.com/en-us/library/bb417456.aspx). Если передается значение null, то возвращаются все элементы списка.|
|**Contains**|Элемент [Contains](http://msdn.microsoft.com/en-us/library/ms196501.aspx), который определяет настройки фильтрации для запроса.|

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md)
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md)
-  [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
-  [Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST](determine-sharepoint-rest-service-endpoint-uris.md)
-  [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [Справочные материалы по интерфейсу API службы REST и примеры](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [Получение версий списков документов с помощью значений ETag в службе REST](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

