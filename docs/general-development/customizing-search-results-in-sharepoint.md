---
title: "Настройка результатов поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1b30f6df-643a-4570-ae5c-d3d8df5609b8
ms.openlocfilehash: 66856c768d51d8de633bc7419148aa9d8b48a7e8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="customizing-search-results-in-sharepoint"></a>Настройка результатов поиска в SharePoint
Узнайте, как для группировки схожих элементов или удаление повторяющихся элементов в списке поиска результатов в SharePoint, эти результаты можно представить в виде краткие и для чтения.
В результатах поиска группировки сворачивает два или более аналогичные элементов в результате поиска со значением для их отображения удобства чтения для пользователя. Удаления дубликатов из результатов поиска является частью группировки, где элементов, которые являются идентичными или почти идентичен удаляются из набора результатов. В зависимости от настроек, заданных администратором SharePoint пользователь может иметь возможность более поздней версии развернуть набора результатов поиска и просмотреть результаты для отдельных, которые были свернуты.
  
    
    

Ниже приведены примеры способов группы результатов поиска:
- Дублируется определение, где почти идентичен документы удаляются из набора результатов.
    
  
- Сайт свертывание, где показано наиболее подходящих элементов, обнаруженных в каждом сайте в наборе результатов.
    
  
- Набор документов свертывание, где отображается только один сбора данных для каждой библиотеки документов в SharePoint.
    
  
Можно указать критерии Свертывание или повторений программным путем с помощью следующих свойств  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) в объектной модели запросов:
-  [CollapseSpecification](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.CollapseSpecification.aspx)
    
  
-  [TrimDuplicates](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.TrimDuplicates.aspx)
    
  
-  [TrimDuplicatesOnProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesOnProperty.aspx)
    
  
-  [TrimDuplicatesKeepCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesKeepCount.aspx)
    
  
-  [TrimDuplicatesIncludeId](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesIncludeId.aspx)
    
  

## <a name="collapse-similar-search-results-using-the-collapsespecification-property"></a>Сворачивание аналогичное результатов поиска с помощью свойства CollapseSpecification
<a name="bk_collapse_specification"> </a>

Принимает свойства **CollapseSpecification**, параметр _Spec_, который может содержать несколько полей, разделенных запятыми или пробела, который вычисляется вместе задать критерии, используемые для сворачивания.
  
    
    
 **Синтаксис**
  
    
    
 `CollapseSpecification = Spec`
  
    
    
В следующей таблице приведены поля параметр  _Spec_.
  
    
    

**В таблице 1. Поля со спецификациями параметров**


|**Элемент в параметре**|**Описание**|
|:-----|:-----|
| _Spec_ <br/> | `Subspec(<space>Subspec)*` <br/> |
| _Subspec_ <br/> | `Prop(','Prop)*[':'Dups]` <br/> |
| _Prop_ <br/> |Управляемое свойство или псевдонима управляемого свойства.  _Prop_ без учета регистра. Управляемое свойство, которое должно быть возможность запроса и возможность сортировки или refineable.<br/> |
| _Dups_ <br/> |Целое число, указывающее количество элементов для сохранения. Значение по умолчанию  1.  <br/> |
| _<space>_ <br/> |Свойства объединяются с помощью оператора **OR**. <br/> |
| _,_ <br/> |Свойства объединяются с помощью оператора **AND**. <br/> |
| _*_ <br/> |Указывает число элементов.  <br/> |
| _() or []_ <br/> |Указывает дополнительные элементы.  <br/> |
   
Если поля в  _Spec_, разделенных запятыми, поля объединяются с помощью оператора **AND**. При выполнении всех указанных полей свернуты элементы.
  
    
    
С другой стороны Если поля в  _Spec_, разделенных пробелами, поля (или _Subspecs_) объединяются с помощью расширения, включая оператор **AND** и **OR** оператор. Например выражение, например `Category:3 Product:2` во внутреннем преобразуется в следующие выражения `(Category AND Product) OR (Category)` со счетчиком для каждого из них; Поэтому не более двух предыдущее и три последних. Элементы свернуты при выполнении некоторых из указанного поля.
  
    
    

### <a name="examples-of-using-collapsespecification"></a>Примеры использования CollapseSpecification

В следующей таблице показаны каталог продукции компании Contoso. Далее задайте примеры использования этого каталога, чтобы показать, как работает свойство **CollapseSpecification**.
  
    
    


|**Категория**|**Продукт**|**Variant**|**Название**|
|:-----|:-----|:-----|:-----|
|Ноутбуки  <br/> |WWI  <br/> |Черный X 0196 19W  <br/> |Компьютер 1  <br/> |
|Ноутбуки  <br/> |AdventureWorks  <br/> |12 M1201 красный  <br/> |Компьютер 2  <br/> |
|Ноутбуки  <br/> |AdventureWorks  <br/> |15,4 Вт Технический M1548  <br/> |Компьютер 3  <br/> |
|Ноутбуки  <br/> |Proseware  <br/> |19 x 910 черный  <br/> |Компьютер 4  <br/> |
|Ноутбуки  <br/> |Proseware  <br/> |Laptop19 X 910 черный  <br/> |Компьютер 5  <br/> |
|Настольные ПК.  <br/> |AdventureWorks  <br/> |2,33 XD233 серебро  <br/> |Компьютер 6  <br/> |
|Настольные ПК.  <br/> |WWI  <br/> |2,33 x черный 2330  <br/> |Компьютер 7  <br/> |
|Настольные ПК.  <br/> |AdventureWorks  <br/> |1.60 Технический ED160  <br/> |Компьютер 8  <br/> |
|Настольные ПК.  <br/> |WWI  <br/> |3.0 серебро M0300  <br/> |Компьютер 9  <br/> |
   

  
    
    

#### <a name="example-group-by-category"></a>Пример: группа по категориям

Во-первых, сгруппировать элементы, в зависимости от **Category** и Показать двух верхних (следовательно `"Category:2"`) для каждой группы. Отобразите соответствующее число уникальных для каждого **Category**(следовательно "Продукта: 1") **Products**.
  
    
    
 **Синтаксис**
  
    
    
 `CollapseSpecification="Category:2 Product:1"`
  
    
    
Это должен возвращать следующие результаты.
  
    
    


|**Категория**|**Продукт**|**Variant**|**Название**|
|:-----|:-----|:-----|:-----|
|Ноутбуки  <br/> |WWI  <br/> |Черный X 0196 19W  <br/> |Компьютер 1  <br/> |
|Ноутбуки  <br/> |Adventure  <br/> |12 M1201 красный  <br/> |Компьютер 2  <br/> |
|Настольные ПК.  <br/> |AdventureWorks  <br/> |2,33 XD233 серебро  <br/> |Компьютер 6  <br/> |
|Настольные ПК.  <br/> |WWI  <br/> |2,33 x черный 2330  <br/> |Компьютер 7  <br/> |
   
Чтобы свернуть результаты поиска с помощью свойства **CollapseSpecification**, используйте следующий код.
  
    
    



```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
        {
            QueryText = "Title:Computer",
            CollapseSpecification = "Category:3 Product:1",
        };

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    {
        Console.WriteLine(result["Title"]);
    }
}

```


#### <a name="example-group-by-category-and-product"></a>Пример: группа по категориям и продукта

Во-первых группы элементов, на основе **Category** и **Product**. Затем щелкните Показать каждого уникальную комбинацию.
  
    
    
 **Синтаксис**
  
    
    
 `CollapseSpecification="Category,Product:1"`
  
    
    
Это должен возвращать следующие результаты.
  
    
    


|**Категория**|**Продукт**|**Variant**|**Название**|
|:-----|:-----|:-----|:-----|
|Ноутбуки  <br/> |WWI  <br/> |Черный X 0196 19W  <br/> |Компьютер 1  <br/> |
|Ноутбуки  <br/> |AdventureWorks  <br/> |12 M1201 красный  <br/> |Компьютер 2  <br/> |
|Ноутбуки  <br/> |Proseware  <br/> |19 x 910 черный  <br/> |Компьютер 4  <br/> |
|Настольные ПК.  <br/> |AdventureWorks  <br/> |2,33 XD233 серебро  <br/> |Компьютер 6  <br/> |
|Настольные ПК.  <br/> |WWI  <br/> |2,33 x черный 2330  <br/> |Компьютер 7  <br/> |
   

## <a name="trim-duplicate-search-results-using-the-trimduplicates-property"></a>Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicates
<a name="bk_trim_duplicates"> </a>

Позволяет указать для удаления повторяющихся поиска результаты из результат установил ли **TrimDuplicates**. **TrimDuplicates**  **true** по умолчанию.
  
    
    
При использовании **TrimDuplicates** с **TrimDuplicatesOnProperty** или желательно **CollapseSpecification** **TrimDuplicates** задано значение **false**.
  
    
    
 **Синтаксис**
  
    
    
 `TrimDuplicates = <$true | $false>`
  
    
    

### <a name="trim-duplicate-search-results-using-the-trimduplicatesonproperty-property"></a>Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicatesOnProperty
<a name="bk_trim_duplicates_on_property"> </a>

Используйте **TrimDuplicatesOnProperty**, чтобы указать, будет ли для использования не по умолчанию управляемого свойства в качестве основы для удаления повторений. Значение по умолчанию  **DocumentSignature** управляемых свойств. Управляемое свойство, которое должен иметь тип **Integer** или **String**. С помощью управляемого свойства, который представляет группировку элементов, этот компонент можно использовать для сворачивания поля.
  
    
    
 **Синтаксис**
  
    
    
 `TrimDuplicatesOnProperty = <managed property>`
  
    
    

> **Примечание:** В SharePoint используйте **CollapseSpecification** , где это возможно. **TrimDuplicatesOnProperty** доступна только в целях обратной совместимости.
  
    
    


### <a name="trim-duplicate-search-results-using-the-trimduplicateskeepcount-property"></a>Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicatesKeepCount
<a name="bk_trim_duplicates_keep_count"> </a>

Позволяет указать число документов, сохраняемых при **TrimDuplicates**  это **true** **TrimDuplicatesKeepCount**. Если **TrimDuplicates** основано на управляемое свойство, которое можно использовать в качестве идентификатора группы, например идентификатор сайта, можно управлять число результатов, возвращаемых для каждой группы. Возвращаемые элементы, с наибольшим динамического ранга в каждой группе.
  
    
    
 **Синтаксис**
  
    
    
 `TrimDuplicatesKeepCount = <number>`
  
    
    

### <a name="retrieve-duplicate-search-results-using-the-trimduplicatesincludeid-property"></a>Получение результатов поиска дубликатов, с помощью свойства TrimDuplicatesIncludeId
<a name="bk_trim_duplicates_include_id"> </a>

Использование **TrimDuplicatesIncludeId** для получения копии документа, когда **TrimDuplicates** **true** и **TrimDuplicatesOnProperty** или **CollapseSpecification** задано значение **false**.
  
    
    
Идентификатор документа,  _docid_используется для извлечения дубликатов определенного документа.
  
    
    
 **Синтаксис**
  
    
    
 `TrimDuplicatesIncludeId = <docid>`
  
    
    

> **Примечание:** _Fcoid_ управляемого свойства в FAST Search Server 2010 for SharePoint заменена _docid_ управляемых свойств в SharePoint.
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx)
    
  
-  [Обзор схемы поиска в SharePoint](http://technet.microsoft.com/en-us/library/jj219669%28office.15%29.aspx)
    
  

  
    
    

