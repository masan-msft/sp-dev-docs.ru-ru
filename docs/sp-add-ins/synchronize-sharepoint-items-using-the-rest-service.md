---
title: "Синхронизация элементов SharePoint с помощью службы REST"
description: "Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса GetListItemChangesSinceToken, входящего в состав службы REST в SharePoint."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 18386524bca492930001b457f065bac39dce7699
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a>Синхронизация элементов SharePoint с помощью службы REST

Синхронизировать элементы между SharePoint и надстройками или службами можно с помощью ресурса **GetListItemChangesSinceToken**. **GetListItemChangesSinceToken** — это элемент службы SharePoint REST, соответствующий вызову веб-службы **Lists.GetListItemChangesSinceToken**.

Выполните запрос **POST**, тело которого содержит объект [Свойства объекта SP.ChangeLogItemQuery](#bk_props).

Запрос вернет XML-файл с **набором строк** объектов ADO, которые соответствуют любым изменениям элементов списка, соответствующим указанному запросу. Дополнительные сведения об этих свойствах, в том числе сведения о возвращаемых значениях, структурах данных свойств и описание элементов CAML, см. в статье [Lists.GetListItemChangesSinceToken](https://msdn.microsoft.com/ru-RU/library/office/jj247029.aspx).

### <a name="example"></a>Пример

**Пример запроса**

`POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`

**Пример тела запроса POST**

```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '
      <Query>
      <Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>'</Query>,
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

<br/>

<a name="bk_props"> </a>

## <a name="spchangelogitemquery-object-properties"></a>Свойства объекта SP.ChangeLogItemQuery

|**Свойство**|**Описание**|
|:-----|:-----|
|**ListName**|Строка, которая содержит название или GUID для списка. При запросе таблицы UserInfo строка содержит UserInfo. Использование GUID приводит к повышению производительности.|
|**ViewName**|Строка, содержащая GUID представления, которое необходимо использовать для атрибутов по умолчанию, представленных параметрами _query_, _viewFields_ и _rowLimit_. Если этот аргумент не указан, используется представление по умолчанию.<br/><br/>Если же он указан, значение параметра _query_, _viewFields_ или _rowLimit_ переопределяет соответствующее значение в представлении.<br/><br/>Например, если в представлении, заданном с помощью параметра _viewFields_, установлено ограничение на количество строк 100, но параметр _rowLimit_ содержит значение 1000, то в ответе будет 1000 строк.|
|**Query**|Элемент [Query](http://msdn.microsoft.com/ru-RU/library/ms471093.aspx), содержащий запрос, который определяет, какие записи возвращаются и в каком порядке.|
|**QueryOptions**|Фрагмент XML следующей формы, содержащий отдельные узлы для различных свойств объекта **SPQuery**:|
|**ChangeToken**|Строка, содержащая токен изменений для запроса.<br/><br/>Описание формата этой строки см. в статье [Обзор журнала изменений](http://msdn.microsoft.com/ru-RU/library/bb417456.aspx). Если передается значение NULL, то возвращаются все элементы списка.|
|**Contains**|Элемент [Contains](http://msdn.microsoft.com/ru-RU/library/ms196501.aspx), который определяет настройки фильтрации для запроса.|

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [Получение версий списков документов с помощью значений ETag в службе REST](working-with-lists-and-list-items-with-rest.md#using-etag-values-to-determine-document-and-list-item-versioning)
- [Справочные материалы по REST API и примеры](https://msdn.microsoft.com/library)
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)

    
 

 

 

