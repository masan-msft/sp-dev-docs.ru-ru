---
title: "Уточнение запросов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ec31782e-1bc5-4dc3-8df7-c29cd5f7f05c
ms.openlocfilehash: 06540ee8f250723ed64d0d56b6891a881f30478d
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="query-refinement-in-sharepoint"></a>Уточнение запросов в SharePoint
Узнайте, как программным путем использования функций уточнения запроса SharePoint при работе с запросы и результаты поиска.
Функций уточнения запроса можно использовать для предоставления конечных пользователей с помощью параметров уточнения результатов поиска, которые относятся к свои запросы. Эти компоненты позволяют конечному пользователю детализации результатов поиска с помощью данных уточнения, вычисленные для результата. Данные уточнения рассчитывается компонентом индекса на основе на объединении статистики управляемого свойства для всех результатов поискового запроса.
  
    
    

Как правило уточнение запроса используется для метаданные, связанные с индексированных элементов, таких как Дата создания, автор или типов файлов, которые отображаются в элементе. С помощью параметров уточнения результатов поиска, можно уточнить запрос для отображения только элементы, созданные в течение определенного периода времени или отображаемые элементы только из определенного типа файлов.
## <a name="using-refiners-in-the-query-object-model"></a>Использование уточнений в объектной модели запросов
<a name="SP15_Using_refiners"> </a>

Состоит из двух запросов уточнение запроса:
  
    
    

1. Можно запросить для набора уточнений возвращаемых в результатах поиска путем  [добавления спецификации уточнения](#SP15_Adding_refiners) запроса конечного пользователя. Спецификация уточнения имеет входные данные для свойства [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) . Этот запрос будет выполняться для индекса поиска. Результаты поиска будет состоять из релевантные результаты и данных уточнения.
    
  
2. Можно использовать данные уточнения в результатах поиска,  [Создание уточненного запроса](#SP15_Creating_refined_query). Добавьте свойство  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) в запрос, чтобы результаты поиска окончательный будут отвечать требованиям обоих исходного текста запроса из конечного пользователя и параметра выбранные уточнения на основе данных уточнения результатов поиска.
    
  
В следующих разделах описываются эти действия подробно и предоставлены примеры кода.
  
    
    

## <a name="adding-refiners-to-the-end-users-query-by-using-refiner-specs"></a>Добавление уточнений в запрос конечного пользователя с помощью спецификации уточнения
<a name="SP15_Adding_refiners"> </a>

Можно указать уточнения запроса с помощью свойства  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) класса [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) . Используйте следующий синтаксис для указания уточнения запроса:
  
    
    
 `<refiner>[,<refiner>]*`
  
    
    

  
    
    
Каждый  `refiner` имеет следующий формат:
  
    
    
 `<refiner-name>[(parameter=value[,parameter=value]*)]?`
  
    
    

  
    
    
где:
  
    
    

-  `<refiner-name>`  это имя управляемого свойства, связанного с уточнением. Это управляемое свойство должно иметь значение [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) или [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) в схеме поиска.
    
  
- Необязательный список пар  `parameter=value` указывает значений конфигурации не по умолчанию для именованного уточнения. Если параметр для уточнения не указан в скобках, конфигурация схемы поиска предоставляет по умолчанию. В таблице 1 перечислены возможные значения для пары `parameter=value` .
    
> [!NOTE]
> При указании уточнений, необходимо как минимум, для указания `refiner-name`, которая является управляемого свойства. 

**Пример**

`Refiners = "FileType"` 
 
 Или можно также использовать расширенный синтаксис для применения настроек уточнения. 

 **Пример**

 `Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22),companies"`
  
    
    


**Таблица 1: Список параметров для уточнения**


|**Параметр**|**Описание**|
|:-----|:-----|
| _deephits_ <br/>|Переопределяет по умолчанию число попаданий, который используется в качестве основы для уточнения вычислений. Когда производятся уточнений, будет выполняться вычисление всех результатов для запроса. Как правило с помощью этого параметра улучшит производительность поиска.<br/>**Синтаксис** <br/>`deephits=<integer value>` <br/>**Пример** <br/>`price(deephits=1000)` <br/>**Примечание**: это ограничение применяется в пределах каждого раздела индекса. Фактическое число обращений, которые вычисляются будет больше, чем это значение из-за объединение в разделах поиска.           |
| _discretize_ <br/>| Задает нестандартные интервалы (контейнеры уточнения) для числовых уточнений. <br/>**Синтаксис** <br/>`discretize=manual/<threshold>/<threshold>[/<threshold>]*` <br/>**Пример** <br/>`write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22)` <br/>Атрибут  `<threshold>` Задает пороговое значение для каждого контейнера уточнения. <br/>Существует один интервал для всех значений ниже первого заданного порогового значения, по одному интервалу между каждыми двумя последовательными пороговыми значениями и один интервал для всех значений выше последнего порогового значения. <br/>Для уточнения типа **DateTime**, пороговое значение указывается в соответствии с одним из следующих ISO 8601 форматами:  <br/><ul><li><i>YYYY-MM-DD</i></li><li><i>YYYY-MM-DDThh:mm:ss</i></li><li><i>YYYY-MM-DDThh:mm:ss:Z</i></li></ul>Значения формата задают следующее. <ul><li><i>YYYY</i> - год из четырех цифр. Поддерживаются только цифрами.</li><li><i>MM</i> - месяца из двух цифр. 01 = января.</li><li><i>DD</i> - из двух цифр день месяца (от 01 до 31). </li><li><i>T</i>  буква "T". </li><li><i>hh</i> - час из двух цифр (00 - 23). Указывает A.M. или P.M., не разрешено.</li><li><i>mm</i> - из двух цифр минуты (от 00 до 59). </li><li><i>ss</i> - из двух цифр второй (от 00 до 59). </li></ul>**Важные:**  Все значения даты и времени должен быть указан согласно по Гринвичу (UTC), также известной как среднее время по Гринвичу (GMT) зоны. Идентификатор зоны UTC (конечные знак «Z») является необязательным.          |
| _sort_ <br/>| Определяет порядок сортировки контейнеров в уточнении строчного типа. <br/>**Синтаксис** <br/>`sort=<property>/<direction>` <br/>Атрибуты выполните следующие настройки: <ul><li><i> \<свойство\> </i> -указывает алгоритм сортировки. Допустимы следующие строчная значения: <ul><li>**frequency**  Сортировка в порядке появления в контейнерах. </li><li>**name**  Сортировка по имени метки. </li><li>**number** - рассматривается как числовых строк и использует числовой сортировки. Это значение можно использовать для указания отдельных значений, например, чтобы выполнить сортировку числовые значения, содержащиеся в управляемое свойство типа **String**. </li></ul></li><li><i> \<направление\> </i> -указывает направление сортировки. Допустимы следующие строчная значения: <ul><li>**descending** </li><li>**ascending** </li></ul></li></ul>**Пример** <br/>`sort=name/ascending` <br/>Значение по умолчанию: **Default** frequency/descending.  <br/>|
| _filter_ <br/>| Определяет порядок фильтрации контейнеров в уточнении типа **String** перед их возвращением клиенту. <br/>**Синтаксис** <br/> `filter=<bins>/<freq>/<prefix>[<levels>]` <br/>Атрибуты выполните следующие настройки: <ul><li><i> \<контейнеров\> </i> -указывает максимальное число возвращаемых контейнеров. <br/>После сортировки корзин в уточнении типа, этот атрибут используется для усечения все конечные ячейки. Например если ячейки = 10, возвращаются только первые 10 ячеек, в соответствии с указанным алгоритм сортировки. </li><li><i> \<freq\> </i> -ограничивает число возвращаемых контейнеров. <br/>Этот атрибут используется для удаления контейнеров с низким значением счетчика частоты. Например,  <i>freq</i>= 2 указывает, что только контейнеры с двумя или более членами возвращаются.</li><li><i> \<префикс\> </i> -указывает, что возвращаются только контейнеры, имена которых начинаются с данного префикса. <br/>Подстановочный знак "\*" будет соответствовать всем именам. <br/>**Пример** <br/>`filter=30/2/*` </li><li><i> \<уровни\> </i> — задает уровни таксономии. <br/>Этот атрибут используется для фильтрации иерархических выходных данных уточнения на основе уровней таксономии. Атрибут должно быть положительное целое число <i>n</i>. Значение **по умолчанию** — <i>n</i>= 0. Если <i>n</i> \>0, только уточнения записей, которые содержат меньше, чем <i>n</i> будут возвращены символы разделителя таксономии путь («/»). Если <i>n</i>= 0, уровня фильтрация не выполняется. Разделителем уровней является символ косой черты («/»).  <br/>Необходимо учитывать производительность с помощью навигатор больших таксономии. Фильтрация данных выполняется в процессе обработки результатов.</li></ul>**Примечание**: этот параметр применяется фильтрация результатов со стороны конкретного приложения. Это отличается от прекращения параметр, который применяет ограничения в каждый раздел индекса для повышения производительности.          |
| _cutoff_ <br/>| Ограничения для данных, который должен передаваться и обработки для уточнения глубокой строки. Вы можете настроить уточнения для возвращения только самые точные значения (контейнеры).<br/>**Примечание**: этот прекращения фильтрация выполняется в рамках каждого раздела индекса. Это отличается от параметр _filter_ , который выполняет фильтрацию только на стороне результатов. Можно объединять два параметра. <br/>**Синтаксис** <br/>`cutoff=<frequency>/<minbins>/<maxbins>` <br/>Атрибуты выполните следующие настройки: <ul><li><i> \<maxbins\> </i> -ограничивает число контейнеров. <br/>Этот параметр ограничивает число уникальных значений (контейнеры), которые будут возвращены для уточнения. Это основной способ для повышения производительности поиска при возвращении уточнений строку с большим количеством ячеек. При значении «0» используется значение по умолчанию, заданное в схеме поиска.</li><li><i> \<частота\> </i> -ограничивает число контейнеров по частоте. <br/>Если число вхождений значения уточнения в результирующий набор меньше или равно значению frequency, значение уточнения не возвращается. При значении «0» используется значение по умолчанию определяется в схеме поиска.</li><li><i> \<minbins\> </i> -задает минимальное значение ограничения по частоте. <br/>Если количество значений уникальных уточнения запроса меньше, чем это значение, не ограничения частота не выполняется и с этого раздела поиска возвращаются все значения уточнения. При использовании Отсечка по частоте этот параметр можно использовать для указания минимальное число уникальных уточнения значения, которые будут возвращены независимо от того, число вхождений. Значение по умолчанию этот атрибут является «0», которое указывает частоту сканирования выполняется независимо от количества уникальных навигатор значения. При значении «0» используется значение по умолчанию, заданное в схеме индекса.</li></ul>**Примечание**: использование _ \<частота\> _ и _ \<minbins\> _ с осторожностью. Мы рекомендуем использовать только _ \<maxbins\>_.           |
   

### <a name="example-adding-refiners"></a>Пример: Добавление уточнений
<a name="SP15_Example_adding_refiners"> </a>

В следующем примере CSOM показано, как программно запросить три уточнения: **FileType**, **Write**и **Companies**. **Write** представляет дату последнего изменения элемента и использует расширенный синтаксис для возврата фиксированного размера ячеек даты и времени.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-
            15/2013-09-21/2013-09-22),companies"
    };
    
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];          
    Console.WriteLine(refinerResultsTable.RowCount + " refinement options:");
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'", 
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }
}
```


## <a name="understanding-the-refinement-data-in-the-search-result"></a>Общие сведения о данных уточнения в результатах поиска
<a name="SP15_Understanding_refinement_data"> </a>

Если вы включили уточнение запроса для управляемого свойства в запросе, результат запроса содержит данные уточнения разделены на корзины уточнения. Эти данные находятся в таблице **RefinementResults** ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) в [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . Одна ячейка уточнения представляет определенное значение или диапазон значений для управляемого свойства. Таблица **RefinementResults** содержит одну строку для каждого контейнера уточнения и содержит столбцы, как указано в таблице 2.
  
    
    

**Таблица 2. Данные, возвращаемые для корзин уточнения**


|**Параметр**|**Описание**|
|:-----|:-----|
|**RefinerName** <br/>|Имя средства уточнения запросов.  <br/>|
|**RefinementName** <br/>|Строка, представляющая контейнера уточнения. Эта строка обычно используется при проведении параметры уточнения результатов поиска для пользователей на странице результатов поиска.  <br/>|
|**RefinementValue** <br/>|Форматированная строка от реализации, представляющий уточнение. Эти данные возвращаются для отладки и обычно не является обязательным для клиента.  <br/>|
|**RefinementToken** <br/>|Строка, представляющая контейнера уточнения для использования с **RefinerName** при выполнении уточненного запроса. <br/>|
|**RefinementCount** <br/>|Количество результатов для этого контейнера уточнения. Число элементов (включая дубликатов) представляет эти данные в результатах поиска со значением для данного управляемого свойства, попадает в этом контейнера уточнения.  <br/>|
   

### <a name="example-refinement-data"></a>Пример: Данные уточнения
<a name="SP15_Example_refinement_data"> </a>

В представленной ниже таблице 3 содержит две строки данных уточнения. Первая строка уточнения для сохранения данных индексированных элементов которой параметр тип файла имеет HTML-код. Второй строке содержит уточнения результатов поиска, данные для индексированных элементов, где время последнего изменения из 2013/09/21 до 2013/09/22.
  
    
    

**В таблице 3: Формат и содержимое данных уточнения**


|**RefinerName**|**RefinementName**|**RefinementValue**|**RefinementToken**|**RefinementCount**|
|:-----|:-----|:-----|:-----|:-----|
|FileType  <br/>|Html  <br/>|Html  <br/>|"???? 68746d6c»  <br/>|50553  <br/>|
|запись;  <br/>|Из 2013-09-21T00:00:00Z до 2013-09-22T00:00:00Z  <br/>|Из 2013-09-21T00:00:00Z до 2013-09-22T00:00:00Z  <br/>|диапазон (2013-09-21T00:00:00Z 2013-09-22T00:00:00Z)  <br/>|37  <br/>|
   

## <a name="creating-a-refined-query"></a>Создание уточненного запроса
<a name="SP15_Creating_refined_query"> </a>

Результат поиска представляет параметры уточнения результатов поиска в виде строковые значения или диапазоны значений. Каждый строковое значение или числовое значение диапазона называется контейнера уточненияи каждой корзины уточнения имеет значение связанного **RefinementToken**. Параметр уточнения связан с управляемым свойством, предоставляемый значение **RefinerName**.
  
    
    
Как **RefinementToken**, так и **RefinerName** значения объединяются для создания _refinement filter_ строки. Эта строка представляет фильтр, который можно использовать для ограничения элементов результатов поиска для включения только элементы которых управляемого свойства имеет значение внутри контейнера уточнения. В short:
  
    
    
 `refinement filter = <RefinerName>:<RefinementToken>`
  
    
    
Уточняющие фильтры для уточненного запроса можно обеспечить путем добавления фильтров уточнения свойство  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) класса [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) . Несколько фильтров уточнения позволяют предоставьте многоуровневой перехода в результатах поиска, для применения уточнения на многозначные свойства. Например можно уточнить запрос для элементов, которые имеют два автора - каждый из которых представлен контейнера уточнения -, но исключить элементы, которые имеют только один из авторов.
  
    
    

### <a name="example-1-creating-a-refined-query-for-html-file-types"></a>В примере 1: Создание уточненного запроса для типов файлов HTML

В следующем примере CSOM показано, как для программного выполнения уточнения результатов поиска, чтобы ограничить поиск теми только тип файла HTML. Как уже упоминалось в [Пример: данные уточнения](#SP15_Example_refinement_data), данных уточнения, связанных с этим параметром уточнения имеет **RefinerName** задать _Тип файла_ и **RefinementToken** присвоено значение _«????68746d6c»_.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {        
        QueryText = "home"
    };
    
    query.RefinementFilters.Add("FileType:\\"????68746d6c\\"");
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    var resultCount = 1;
    foreach (var relevantResult in relevantResultsTable.ResultRows)
    {
        Console.WriteLine("Relevant result number {0} has file type {1}.", 
            resultCount, relevantResult["FileType"]);
            resultCount++;
    }
}
```


### <a name="example-2-creating-a-refined-query-by-using-previously-obtained-refinement-data"></a>Пример 2: Создание уточненного запроса с помощью ранее полученные данные уточнения

В следующем примере CSOM показано, как выполнить запрос с помощью спецификации уточнения для создания данных уточнения, который впоследствии используется для выполнения уточнения результатов поиска. В этом примере моделирует процесс конечный пользователь при выборе первого параметра уточнения результатов поиска.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    // Step 1: Run the query with refiner spec to provide refinement data in search result
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/
2013-09-15/2013-09-21/2013-09-22),companies"
    };
    
    Console.WriteLine("Run query '{0}' with refiner spec '{1}'.", query.QueryText,
query.Refiners);
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);
    context.ExecuteQuery();

    // The query has been run and we can now look at the refinement data, to view the
    // refinement options
    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];
    Console.WriteLine("Got back {0} refinement options in the result:",
        refinerResultsTable.RowCount);
    
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'",
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }

    // Step 2: Run the refined query with refinement filter to drill down into 
    // the search results. This example uses the first refinement option in the refinement
    // data, if available. This simulates an end user selecting this refinement option.
    var refinementOptionArray = refinerResultsTable.ResultRows.ToArray();

    if (refinementOptionArray.Length > 0)
    {                         
        var firstRefinementOption = refinementOptionArray[6];
        // Construct the refinement filter by concatenation
        var refinementFilter = firstRefinementOption["RefinerName"] + ":" +
            firstRefinementOption["RefinementToken"];
        var refinedQuery = new KeywordQuery(context)
        {
            QueryText = query.QueryText
        };
        refinedQuery.RefinementFilters.Add(refinementFilter);
        refinedQuery.SelectProperties.Add("FileType");
        refinedQuery.SelectProperties.Add("Write");
        refinedQuery.SelectProperties.Add("Companies");
        Console.WriteLine("Run query '{0}' with refinement filter '{1}'",            
            refinedQuery.QueryText, refinementFilter);
        var refinedResults = executor.ExecuteQuery(refinedQuery);
        context.ExecuteQuery();
        ResultTable refinedRelevantResultsTable = refinedResults.Value[0];
        var resultCount = 1;
        foreach (var relevantResult in refinedRelevantResultsTable.ResultRows)
        {
            Console.WriteLine("Relevant result number {0} has FileType='{1}',
                Write='{2}', Companies='{3}'", 
                resultCount, 
                relevantResult["FileType"],
                relevantResult["Write"],
                relevantResult["Companies"]
            );
            resultCount++;
        }
    }
}
```


## <a name="see-also"></a>См. также
<a name="SP15_Query_refinement_addresources"> </a>


-  [Настройка свойств веб-части уточнения результатов поиска в SharePoint](http://technet.microsoft.com/en-us/library/gg549985.aspx)
    
  
-  [Обзор схемы поиска в SharePoint](http://technet.microsoft.com/en-us/library/jj219669%28office.15%29.aspx)
    
  

## <a name="see-also"></a>См. также
<a name="SP15_Query_refinement_addresources"> </a>


#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Схема индекса (FAST Search Server для SharePoint)](http://msdn.microsoft.com/library/3e1eed3f-8a6f-4911-9607-f1616e6a44f3%28Office.15%29.aspx)
  
    
    
 [Элемент Refiner в схеме Microsoft.Search.Query](http://msdn.microsoft.com/library/0512c17a-18e9-45e3-9061-9dba9cd45ef4%28Office.15%29.aspx)
