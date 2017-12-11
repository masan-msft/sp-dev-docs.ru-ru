---
title: "Уточнение запросов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ec31782e-1bc5-4dc3-8df7-c29cd5f7f05c
ms.openlocfilehash: 379307fb0cb2867e79a74b4dee9e404243d47ddf
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="query-refinement-in-sharepoint"></a><span data-ttu-id="d86ea-102">Уточнение запросов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d86ea-102">Query Refinement in SharePoint</span></span>
<span data-ttu-id="d86ea-103">Узнайте, как программным путем использования функций уточнения запроса SharePoint при работе с запросы и результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-103">Learn how to use SharePoint query refinement features programmatically when you are working with search queries and results.</span></span>
<span data-ttu-id="d86ea-104">Функций уточнения запроса можно использовать для предоставления конечных пользователей с помощью параметров уточнения результатов поиска, которые относятся к свои запросы.</span><span class="sxs-lookup"><span data-stu-id="d86ea-104">You can use query refinement features to provide end users with refinement options that are relevant for their queries.</span></span> <span data-ttu-id="d86ea-105">Эти компоненты позволяют конечному пользователю детализации результатов поиска с помощью данных уточнения, вычисленные для результата.</span><span class="sxs-lookup"><span data-stu-id="d86ea-105">These features let the end user drill down into search results by using refinement data computed for the results.</span></span> <span data-ttu-id="d86ea-106">Данные уточнения рассчитывается компонентом индекса на основе на объединении статистики управляемого свойства для всех результатов поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-106">Refinement data is calculated by the index component, based on the aggregation of managed property statistics for all of the results of a search query.</span></span>
  
    
    

<span data-ttu-id="d86ea-p102">Как правило уточнение запроса используется для метаданные, связанные с индексированных элементов, таких как Дата создания, автор или типов файлов, которые отображаются в элементе. С помощью параметров уточнения результатов поиска, можно уточнить запрос для отображения только элементы, созданные в течение определенного периода времени или отображаемые элементы только из определенного типа файлов.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p102">Typically, query refinement is used for metadata associated with the indexed items, such as creation date, author, or file types that appear in the item. By using the refinement options, you can refine your query to display only items created during a certain time period, or display only items of a specific file type.</span></span>
## <a name="using-refiners-in-the-query-object-model"></a><span data-ttu-id="d86ea-109">Использование уточнений в объектной модели запросов</span><span class="sxs-lookup"><span data-stu-id="d86ea-109">Using refiners in the Query Object Model</span></span>
<span data-ttu-id="d86ea-110"><a name="SP15_Using_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-110"></span></span>

<span data-ttu-id="d86ea-111">Состоит из двух запросов уточнение запроса:</span><span class="sxs-lookup"><span data-stu-id="d86ea-111">There are two queries involved in query refinement:</span></span>
  
    
    

1. <span data-ttu-id="d86ea-p103">Можно запросить для набора уточнений возвращаемых в результатах поиска путем  [добавления спецификации уточнения](#SP15_Adding_refiners) запроса конечного пользователя. Спецификация уточнения имеет входные данные для свойства [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) . Этот запрос будет выполняться для индекса поиска. Результаты поиска будет состоять из релевантные результаты и данных уточнения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p103">You can request for a set of refiners to be returned in the search results by  [adding a refiner spec](#SP15_Adding_refiners) to the end user's query. A refiner spec is the input for the [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) property. This query is run against the search index. The search results will consist of relevant results and refinement data.</span></span>
    
  
2. <span data-ttu-id="d86ea-p104">Можно использовать данные уточнения в результатах поиска,  [Создание уточненного запроса](#SP15_Creating_refined_query). Добавьте свойство  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) в запрос, чтобы результаты поиска окончательный будут отвечать требованиям обоих исходного текста запроса из конечного пользователя и параметра выбранные уточнения на основе данных уточнения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p104">You can use the refinement data to drill down into the search results by,  [creating a refined query](#SP15_Creating_refined_query). Add the  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) property to the query so that the final search results will meet the requirements of both the original query text from the end user and the selected refinement option from the refinement data.</span></span>
    
  
<span data-ttu-id="d86ea-118">В следующих разделах описываются эти действия подробно и предоставлены примеры кода.</span><span class="sxs-lookup"><span data-stu-id="d86ea-118">The following sections describe these steps in detail, and provide code examples.</span></span>
  
    
    

## <a name="adding-refiners-to-the-end-users-query-by-using-refiner-specs"></a><span data-ttu-id="d86ea-119">Добавление уточнений в запрос конечного пользователя с помощью спецификации уточнения</span><span class="sxs-lookup"><span data-stu-id="d86ea-119">Adding refiners to the end-user's query by using refiner specs</span></span>
<span data-ttu-id="d86ea-120"><a name="SP15_Adding_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-120"></span></span>

<span data-ttu-id="d86ea-p105">Можно указать уточнения запроса с помощью свойства  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) класса [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) . Используйте следующий синтаксис для указания уточнения запроса:</span><span class="sxs-lookup"><span data-stu-id="d86ea-p105">You can specify the requested query refiners by using the  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) class. Use the following syntax to specify the requested query refiners:</span></span>
  
    
    
 `<refiner>[,<refiner>]*`
  
    
    

  
    
    
<span data-ttu-id="d86ea-123">Каждый  `refiner` имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d86ea-123">Each  `refiner` has the following format:</span></span>
  
    
    
 `<refiner-name>[(parameter=value[,parameter=value]*)]?`
  
    
    

  
    
    
<span data-ttu-id="d86ea-124">где:</span><span class="sxs-lookup"><span data-stu-id="d86ea-124">Where:</span></span>
  
    
    

-  <span data-ttu-id="d86ea-p106">`<refiner-name>`  это имя управляемого свойства, связанного с уточнением. Это управляемое свойство должно иметь значение [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) или [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) в схеме поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p106">`<refiner-name>` is the name of the managed property associated with the refiner. This managed property must be set to [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) or [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) in the search schema.</span></span>
    
  
- <span data-ttu-id="d86ea-p107">Необязательный список пар  `parameter=value` указывает значений конфигурации не по умолчанию для именованного уточнения. Если параметр для уточнения не указан в скобках, конфигурация схемы поиска предоставляет по умолчанию. В таблице 1 перечислены возможные значения для пары `parameter=value` .</span><span class="sxs-lookup"><span data-stu-id="d86ea-p107">The optional list of  `parameter=value` pairs specifies non-default configuration values for the named refiner. If a parameter for a refiner is not listed inside the parentheses, the search schema configuration gives you the default setting. Table 1 lists possible values for the `parameter=value` pairs.</span></span>
    
> [!NOTE]
> <span data-ttu-id="d86ea-130">При указании уточнений, необходимо как минимум, для указания `refiner-name`, которая является управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="d86ea-130">When you specify refiners, the minimum requirement is to specify a  `refiner-name`, which is a managed property.</span></span> 

<span data-ttu-id="d86ea-131">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-131">**Example**</span></span>

`Refiners = "FileType"` 
 
 <span data-ttu-id="d86ea-132">Или можно также использовать расширенный синтаксис для применения настроек уточнения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-132">Or, you can also use the advanced syntax to adjust the refiner settings.</span></span> 

 <span data-ttu-id="d86ea-133">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-133">**Example**</span></span>

 `Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22),companies"`
  
    
    


<span data-ttu-id="d86ea-134">**Таблица 1: Список параметров для уточнения**</span><span class="sxs-lookup"><span data-stu-id="d86ea-134">**Table 1: List of parameters for refiners**</span></span>


|<span data-ttu-id="d86ea-135">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="d86ea-135">**Parameter**</span></span>|<span data-ttu-id="d86ea-136">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d86ea-136">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="d86ea-137">_deephits_</span><span class="sxs-lookup"><span data-stu-id="d86ea-137">_deephits_</span></span> <br/>|<span data-ttu-id="d86ea-p108">Переопределяет по умолчанию число попаданий, который используется в качестве основы для уточнения вычислений. Когда производятся уточнений, будет выполняться вычисление всех результатов для запроса. Как правило с помощью этого параметра улучшит производительность поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p108">Overrides the default number of hits that is used as the basis for refinement computation. When refiners are produced, all results for the query will be evaluated. Normally, using this parameter will improve search performance.  </span></span><br/><span data-ttu-id="d86ea-141">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d86ea-141">**Syntax**</span></span> <br/>`deephits=<integer value>` <br/><span data-ttu-id="d86ea-142">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-142">**Example**</span></span> <br/>`price(deephits=1000)` <br/><span data-ttu-id="d86ea-143">**Примечание**: это ограничение применяется в пределах каждого раздела индекса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-143">**Note**: This limit applies within each index partition.</span></span> <span data-ttu-id="d86ea-144">Фактическое число обращений, которые вычисляются будет больше, чем это значение из-за объединение в разделах поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-144">The actual number of hits that are evaluated will be larger than this value due to the aggregation across search partitions.</span></span>           |
| <span data-ttu-id="d86ea-145">_discretize_</span><span class="sxs-lookup"><span data-stu-id="d86ea-145">_discretize_</span></span> <br/>| <span data-ttu-id="d86ea-146">Задает нестандартные интервалы (контейнеры уточнения) для числовых уточнений.</span><span class="sxs-lookup"><span data-stu-id="d86ea-146">Specifies custom intervals (refinement bins) for numeric refiners.</span></span> <br/><span data-ttu-id="d86ea-147">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d86ea-147">**Syntax**</span></span> <br/>`discretize=manual/<threshold>/<threshold>[/<threshold>]*` <br/><span data-ttu-id="d86ea-148">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-148">**Example**</span></span> <br/>`write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22)` <br/><span data-ttu-id="d86ea-149">Атрибут  `<threshold>` Задает пороговое значение для каждого контейнера уточнения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-149">The `<threshold>` attribute specifies the threshold for each refinement bin.</span></span> <br/><span data-ttu-id="d86ea-150">Существует один интервал для всех значений ниже первого заданного порогового значения, по одному интервалу между каждыми двумя последовательными пороговыми значениями и один интервал для всех значений выше последнего порогового значения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-150">There is one interval for everything below the first threshold specified, one interval between each consecutive threshold, and one interval for everything above the last threshold.</span></span> <br/><span data-ttu-id="d86ea-151">Для уточнения типа **DateTime**, пороговое значение указывается в соответствии с одним из следующих ISO 8601 форматами:</span><span class="sxs-lookup"><span data-stu-id="d86ea-151">For a refiner of type **DateTime**, specify the threshold according to one of the following ISO 8601-compatible formats:</span></span>  <br/><ul><li><span data-ttu-id="d86ea-152"><i>YYYY-MM-DD</i></span><span class="sxs-lookup"><span data-stu-id="d86ea-152"><i>YYYY-MM-DD</i></span></span></li><li><span data-ttu-id="d86ea-153"><i>YYYY-MM-DDThh:mm:ss</i></span><span class="sxs-lookup"><span data-stu-id="d86ea-153"><i>YYYY-MM-DDThh:mm:ss</i></span></span></li><li><span data-ttu-id="d86ea-154"><i>YYYY-MM-DDThh:mm:ss:Z</i></span><span class="sxs-lookup"><span data-stu-id="d86ea-154"><i>YYYY-MM-DDThh:mm:ss:Z</i></span></span></li></ul><span data-ttu-id="d86ea-155">Значения формата задают следующее.</span><span class="sxs-lookup"><span data-stu-id="d86ea-155">The format values specify the following:</span></span> <ul><li><span data-ttu-id="d86ea-p110"><i>YYYY</i> - год из четырех цифр. Поддерживаются только цифрами.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p110"><i>YYYY</i> - Four-digit year. Only four-digit years are supported. </span></span></li><li><span data-ttu-id="d86ea-p111"><i>MM</i> - месяца из двух цифр. 01 = января.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p111"><i>MM</i> - Two-digit month. 01 = January. </span></span></li><li><span data-ttu-id="d86ea-160"><i>DD</i> - из двух цифр день месяца (от 01 до 31).</span><span class="sxs-lookup"><span data-stu-id="d86ea-160"><i>DD</i> - Two-digit day of month (01 through 31).</span></span> </li><li><span data-ttu-id="d86ea-161"><i>T</i>  буква "T".</span><span class="sxs-lookup"><span data-stu-id="d86ea-161"><i>T</i> - The letter "T".</span></span> </li><li><span data-ttu-id="d86ea-p112"><i>hh</i> - час из двух цифр (00 - 23). Указывает A.M. или P.M., не разрешено.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p112"><i>hh</i> - Two-digit hour (00 through 23). A.M. or P.M. indication is not allowed. </span></span></li><li><span data-ttu-id="d86ea-166"><i>mm</i> - из двух цифр минуты (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="d86ea-166"><i>mm</i> - Two-digit minute (00 through 59).</span></span> </li><li><span data-ttu-id="d86ea-167"><i>ss</i> - из двух цифр второй (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="d86ea-167"><i>ss</i> - Two-digit second (00 through 59).</span></span> </li></ul><span data-ttu-id="d86ea-168">**Важные:**  Все значения даты и времени должен быть указан согласно по Гринвичу (UTC), также известной как среднее время по Гринвичу (GMT) зоны.</span><span class="sxs-lookup"><span data-stu-id="d86ea-168">**Important:**  All date/time values must be specified according to the Coordinated Universal Time (UTC), also known as Greenwich Mean Time (GMT) zone.</span></span> <span data-ttu-id="d86ea-169">Идентификатор зоны UTC (конечные знак «Z») является необязательным.</span><span class="sxs-lookup"><span data-stu-id="d86ea-169">The UTC zone identifier (a trailing "Z" character) is optional.</span></span>          |
| <span data-ttu-id="d86ea-170">_sort_</span><span class="sxs-lookup"><span data-stu-id="d86ea-170">_sort_</span></span> <br/>| <span data-ttu-id="d86ea-171">Определяет порядок сортировки контейнеров в уточнении строчного типа.</span><span class="sxs-lookup"><span data-stu-id="d86ea-171">Defines how to sort the bins within a string refiner.</span></span> <br/><span data-ttu-id="d86ea-172">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d86ea-172">**Syntax**</span></span> <br/>`sort=<property>/<direction>` <br/><span data-ttu-id="d86ea-173">Атрибуты выполните следующие настройки:</span><span class="sxs-lookup"><span data-stu-id="d86ea-173">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="d86ea-174"><i> \<свойство\> </i> -указывает алгоритм сортировки.</span><span class="sxs-lookup"><span data-stu-id="d86ea-174"><i>\<property\></i> - Specifies the sorting algorithm.</span></span> <span data-ttu-id="d86ea-175">Допустимы следующие строчная значения:</span><span class="sxs-lookup"><span data-stu-id="d86ea-175">These lowercase values are valid:</span></span> <ul><li><span data-ttu-id="d86ea-176">**frequency**  Сортировка в порядке появления в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="d86ea-176">**frequency** - Orders by occurrence within the bins.</span></span> </li><li><span data-ttu-id="d86ea-177">**name**  Сортировка по имени метки.</span><span class="sxs-lookup"><span data-stu-id="d86ea-177">**name** - Orders by label name.</span></span> </li><li><span data-ttu-id="d86ea-p115">**number** - рассматривается как числовых строк и использует числовой сортировки. Это значение можно использовать для указания отдельных значений, например, чтобы выполнить сортировку числовые значения, содержащиеся в управляемое свойство типа **String**. </span><span class="sxs-lookup"><span data-stu-id="d86ea-p115">**number** - Treats the strings as numeric and uses numeric sorting. This value can be useful to specify discrete values, for example, to perform numeric sorting of a value that is contained in a managed property of type **String**.</span></span></li></ul></li><li><span data-ttu-id="d86ea-180"><i> \<направление\> </i> -указывает направление сортировки.</span><span class="sxs-lookup"><span data-stu-id="d86ea-180"><i>\<direction\></i> - Specifies the sorting direction.</span></span> <span data-ttu-id="d86ea-181">Допустимы следующие строчная значения:</span><span class="sxs-lookup"><span data-stu-id="d86ea-181">These lowercase values are valid :</span></span> <ul><li><span data-ttu-id="d86ea-182">**descending**</span><span class="sxs-lookup"><span data-stu-id="d86ea-182">**descending**</span></span> </li><li><span data-ttu-id="d86ea-183">**ascending**</span><span class="sxs-lookup"><span data-stu-id="d86ea-183">**ascending**</span></span> </li></ul></li></ul><span data-ttu-id="d86ea-184">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-184">**Example**</span></span> <br/>`sort=name/ascending` <br/><span data-ttu-id="d86ea-185">Значение по умолчанию: **Default** frequency/descending.</span><span class="sxs-lookup"><span data-stu-id="d86ea-185">**Default**: frequency/descending</span></span>  <br/>|
| <span data-ttu-id="d86ea-186">_filter_</span><span class="sxs-lookup"><span data-stu-id="d86ea-186">_filter_</span></span> <br/>| <span data-ttu-id="d86ea-187">Определяет порядок фильтрации контейнеров в уточнении типа **String** перед их возвращением клиенту.</span><span class="sxs-lookup"><span data-stu-id="d86ea-187">Defines how bins within a refiner of type **String** are filtered before they are returned to the client.</span></span> <br/><span data-ttu-id="d86ea-188">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d86ea-188">**Syntax**</span></span> <br/> `filter=<bins>/<freq>/<prefix>[<levels>]` <br/><span data-ttu-id="d86ea-189">Атрибуты выполните следующие настройки:</span><span class="sxs-lookup"><span data-stu-id="d86ea-189">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="d86ea-190"><i> \<контейнеров\> </i> -указывает максимальное число возвращаемых контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d86ea-190"><i>\<bins\></i> - Specifies the maximum number of returned bins.</span></span> <br/><span data-ttu-id="d86ea-191">После сортировки корзин в уточнении типа, этот атрибут используется для усечения все конечные ячейки. Например если ячейки = 10, возвращаются только первые 10 ячеек, в соответствии с указанным алгоритм сортировки.</span><span class="sxs-lookup"><span data-stu-id="d86ea-191">After sorting the bins within the refiner, use this attribute to truncate any trailing bins. For example, if bins=10, only the first 10 bins are returned, according to the specified sorting algorithm.</span></span> </li><li><span data-ttu-id="d86ea-192"><i> \<freq\> </i> -ограничивает число возвращаемых контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d86ea-192"><i>\<freq\></i> - Limits the number of returned bins.</span></span> <br/><span data-ttu-id="d86ea-p117">Этот атрибут используется для удаления контейнеров с низким значением счетчика частоты. Например,  <i>freq</i>= 2 указывает, что только контейнеры с двумя или более членами возвращаются.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p117">Use this attribute to remove bins that have low frequency counts. For example, <i>freq</i>=2 indicates that only the bins with 2 or more members are returned.  </span></span></li><li><span data-ttu-id="d86ea-195"><i> \<префикс\> </i> -указывает, что возвращаются только контейнеры, имена которых начинаются с данного префикса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-195"><i>\<prefix\></i> - Specifies that only bins with a name that begins with this prefix are returned.</span></span> <br/><span data-ttu-id="d86ea-196">Подстановочный знак "\*" будет соответствовать всем именам.</span><span class="sxs-lookup"><span data-stu-id="d86ea-196">The wildcard character "\*" will match all names.</span></span> <br/><span data-ttu-id="d86ea-197">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d86ea-197">**Example**</span></span> <br/>`filter=30/2/*` </li><li><span data-ttu-id="d86ea-198"><i> \<уровни\> </i> — задает уровни таксономии.</span><span class="sxs-lookup"><span data-stu-id="d86ea-198"><i>\<levels\></i> - Specifies the levels of taxonomy.</span></span> <br/><span data-ttu-id="d86ea-199">Этот атрибут используется для фильтрации иерархических выходных данных уточнения на основе уровней таксономии.</span><span class="sxs-lookup"><span data-stu-id="d86ea-199">Use this attribute to filter hierarchical refiner output based on taxonomy levels.</span></span> <span data-ttu-id="d86ea-200">Атрибут должно быть положительное целое число <i>n</i>.</span><span class="sxs-lookup"><span data-stu-id="d86ea-200">The attribute should be a positive integer <i>n</i>.</span></span> <span data-ttu-id="d86ea-201">Значение **по умолчанию** — <i>n</i>= 0.</span><span class="sxs-lookup"><span data-stu-id="d86ea-201">The **default** value is <i>n</i>=0.</span></span> <span data-ttu-id="d86ea-202">Если <i>n</i> \>0, только уточнения записей, которые содержат меньше, чем <i>n</i> будут возвращены символы разделителя таксономии путь («/»).</span><span class="sxs-lookup"><span data-stu-id="d86ea-202">If  <i>n</i>\>0, only refiner entries that contain less than  <i>n</i> taxonomy path separator symbols ("/") will be returned.</span></span> <span data-ttu-id="d86ea-203">Если <i>n</i>= 0, уровня фильтрация не выполняется.</span><span class="sxs-lookup"><span data-stu-id="d86ea-203">If <i>n</i>=0, no level filtering is performed.</span></span> <span data-ttu-id="d86ea-204">Разделителем уровней является символ косой черты («/»).</span><span class="sxs-lookup"><span data-stu-id="d86ea-204">The level separator is the forward slash character ("/").</span></span>  <br/><span data-ttu-id="d86ea-p119">Необходимо учитывать производительность с помощью навигатор больших таксономии. Фильтрация данных выполняется в процессе обработки результатов.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p119">Be aware of the performance cost of using a large taxonomy navigator. The filtering is performed as part of the result processing. </span></span></li></ul><span data-ttu-id="d86ea-207">**Примечание**: этот параметр применяется фильтрация результатов со стороны конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-207">**Note**:  This parameter applies application-specific result-side filtering.</span></span> <span data-ttu-id="d86ea-208">Это отличается от прекращения параметр, который применяет ограничения в каждый раздел индекса для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="d86ea-208">This differs from the cutoff parameter, which applies limitations in every index partition for performance reasons.</span></span>          |
| <span data-ttu-id="d86ea-209">_cutoff_</span><span class="sxs-lookup"><span data-stu-id="d86ea-209">_cutoff_</span></span> <br/>| <span data-ttu-id="d86ea-p121">Ограничения для данных, который должен передаваться и обработки для уточнения глубокой строки. Вы можете настроить уточнения для возвращения только самые точные значения (контейнеры).</span><span class="sxs-lookup"><span data-stu-id="d86ea-p121">Limits the data that must be transferred and processed for deep string refiners. You can configure the refiners to return only the most relevant values (bins). </span></span><br/><span data-ttu-id="d86ea-212">**Примечание**: этот прекращения фильтрация выполняется в рамках каждого раздела индекса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-212">**Note**:  This cutoff filtering is performed within each index partition.</span></span> <span data-ttu-id="d86ea-213">Это отличается от параметр _filter_ , который выполняет фильтрацию только на стороне результатов.</span><span class="sxs-lookup"><span data-stu-id="d86ea-213">This differs from the _filter_ parameter, which performs result-side filtering only.</span></span> <span data-ttu-id="d86ea-214">Можно объединять два параметра.</span><span class="sxs-lookup"><span data-stu-id="d86ea-214">You can combine the two parameters.</span></span> <br/><span data-ttu-id="d86ea-215">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d86ea-215">**Syntax**</span></span> <br/>`cutoff=<frequency>/<minbins>/<maxbins>` <br/><span data-ttu-id="d86ea-216">Атрибуты выполните следующие настройки:</span><span class="sxs-lookup"><span data-stu-id="d86ea-216">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="d86ea-217"><i> \<maxbins\> </i> -ограничивает число контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d86ea-217"><i>\<maxbins\></i> - Limits the number of bins.</span></span> <br/><span data-ttu-id="d86ea-p123">Этот параметр ограничивает число уникальных значений (контейнеры), которые будут возвращены для уточнения. Это основной способ для повышения производительности поиска при возвращении уточнений строку с большим количеством ячеек. При значении «0» используется значение по умолчанию, заданное в схеме поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p123">This parameter limits the number of unique values (bins) that will be returned for a refiner. It is the preferred way to increase search performance when string refiners with large number of bins are returned. "0" implies that the default value specified in the search schema is used. </span></span></li><li><span data-ttu-id="d86ea-221"><i> \<частота\> </i> -ограничивает число контейнеров по частоте.</span><span class="sxs-lookup"><span data-stu-id="d86ea-221"><i>\<frequency\></i> - Limits the number of bins by frequency.</span></span> <br/><span data-ttu-id="d86ea-p124">Если число вхождений значения уточнения в результирующий набор меньше или равно значению frequency, значение уточнения не возвращается. При значении «0» используется значение по умолчанию определяется в схеме поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p124">If the number of occurrences of a refiner value in a result set is less than or equal to the frequency value, the refiner value is not returned. "0" implies that the default value according to the search schema is used. </span></span></li><li><span data-ttu-id="d86ea-224"><i> \<minbins\> </i> -задает минимальное значение ограничения по частоте.</span><span class="sxs-lookup"><span data-stu-id="d86ea-224"><i>\<minbins\></i> - Specifies the minimum value for frequency cutoff.</span></span> <br/><span data-ttu-id="d86ea-p125">Если количество значений уникальных уточнения запроса меньше, чем это значение, не ограничения частота не выполняется и с этого раздела поиска возвращаются все значения уточнения. При использовании Отсечка по частоте этот параметр можно использовать для указания минимальное число уникальных уточнения значения, которые будут возвращены независимо от того, число вхождений. Значение по умолчанию этот атрибут является «0», которое указывает частоту сканирования выполняется независимо от количества уникальных навигатор значения. При значении «0» используется значение по умолчанию, заданное в схеме индекса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p125">If the number of unique refiner values for the query is less than this value, no frequency cutoff is performed, and all refiner values are returned from that search partition. When cutoff by frequency is used, this parameter can be used to specify a minimum number of unique refiner values that will be returned regardless of the number of occurrences. The default value of this attribute is "0", indicating that frequency cutoff is performed regardless of the number of unique navigator values. "0" implies that the default value specified in the index schema is used. </span></span></li></ul><span data-ttu-id="d86ea-229">**Примечание**: использование _ \<частота\> _ и _ \<minbins\> _ с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="d86ea-229">**Note**:  Use _\<frequency\>_ and _\<minbins\>_ with care.</span></span> <span data-ttu-id="d86ea-230">Мы рекомендуем использовать только _ \<maxbins\>_.</span><span class="sxs-lookup"><span data-stu-id="d86ea-230">We recommend that you use only _\<maxbins\>_.</span></span>           |
   

### <a name="example-adding-refiners"></a><span data-ttu-id="d86ea-231">Пример: Добавление уточнений</span><span class="sxs-lookup"><span data-stu-id="d86ea-231">Example: Adding refiners</span></span>
<span data-ttu-id="d86ea-232"><a name="SP15_Example_adding_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-232"></span></span>

<span data-ttu-id="d86ea-p127">В следующем примере CSOM показано, как программно запросить три уточнения: **FileType**, **Write**и **Companies**. **Write** представляет дату последнего изменения элемента и использует расширенный синтаксис для возврата фиксированного размера ячеек даты и времени.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p127">The following CSOM example shows how to programmatically request three refiners: **FileType**, **Write**, and **Companies**. **Write** represents the last modified date for the item, and uses the advanced syntax to return fixed-size date/time bins.</span></span>
  
    
    

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


## <a name="understanding-the-refinement-data-in-the-search-result"></a><span data-ttu-id="d86ea-235">Общие сведения о данных уточнения в результатах поиска</span><span class="sxs-lookup"><span data-stu-id="d86ea-235">Understanding the refinement data in the search result</span></span>
<span data-ttu-id="d86ea-236"><a name="SP15_Understanding_refinement_data"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-236"></span></span>

<span data-ttu-id="d86ea-p128">Если вы включили уточнение запроса для управляемого свойства в запросе, результат запроса содержит данные уточнения разделены на корзины уточнения. Эти данные находятся в таблице **RefinementResults** ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) в [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . Одна ячейка уточнения представляет определенное значение или диапазон значений для управляемого свойства. Таблица **RefinementResults** содержит одну строку для каждого контейнера уточнения и содержит столбцы, как указано в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p128">If you have enabled query refinement for a managed property in your query, the query result contains refinement data split into refinement bins. This data is located in the **RefinementResults** table ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) within the [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . One refinement bin represents a specific value or value range for the managed property.The **RefinementResults** table contains one row per refinement bin, and contains the columns, as specified in Table 2.</span></span>
  
    
    

<span data-ttu-id="d86ea-239">**Таблица 2. Данные, возвращаемые для корзин уточнения**</span><span class="sxs-lookup"><span data-stu-id="d86ea-239">**Table 2: Data returned for refinement bins**</span></span>


|<span data-ttu-id="d86ea-240">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="d86ea-240">**Parameter**</span></span>|<span data-ttu-id="d86ea-241">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d86ea-241">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d86ea-242">**RefinerName**</span><span class="sxs-lookup"><span data-stu-id="d86ea-242">**RefinerName**</span></span> <br/>|<span data-ttu-id="d86ea-243">Имя средства уточнения запросов.</span><span class="sxs-lookup"><span data-stu-id="d86ea-243">The name of the query refiner.</span></span>  <br/>|
|<span data-ttu-id="d86ea-244">**RefinementName**</span><span class="sxs-lookup"><span data-stu-id="d86ea-244">**RefinementName**</span></span> <br/>|<span data-ttu-id="d86ea-p129">Строка, представляющая контейнера уточнения. Эта строка обычно используется при проведении параметры уточнения результатов поиска для пользователей на странице результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p129">The string that represents the refinement bin. This string is typically used when presenting the refinement options to the users on a search result page.</span></span>  <br/>|
|<span data-ttu-id="d86ea-247">**RefinementValue**</span><span class="sxs-lookup"><span data-stu-id="d86ea-247">**RefinementValue**</span></span> <br/>|<span data-ttu-id="d86ea-p130">Форматированная строка от реализации, представляющий уточнение. Эти данные возвращаются для отладки и обычно не является обязательным для клиента.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p130">An implementation-specific formatted string that represents refinement. This data is returned for debugging and is typically not required for the client.</span></span>  <br/>|
|<span data-ttu-id="d86ea-250">**RefinementToken**</span><span class="sxs-lookup"><span data-stu-id="d86ea-250">**RefinementToken**</span></span> <br/>|<span data-ttu-id="d86ea-251">Строка, представляющая контейнера уточнения для использования с **RefinerName** при выполнении уточненного запроса.</span><span class="sxs-lookup"><span data-stu-id="d86ea-251">A string that represents the refinement bin to use with **RefinerName** when you perform a refined query.</span></span> <br/>|
|<span data-ttu-id="d86ea-252">**RefinementCount**</span><span class="sxs-lookup"><span data-stu-id="d86ea-252">**RefinementCount**</span></span> <br/>|<span data-ttu-id="d86ea-p131">Количество результатов для этого контейнера уточнения. Число элементов (включая дубликатов) представляет эти данные в результатах поиска со значением для данного управляемого свойства, попадает в этом контейнера уточнения.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p131">The result count for this refinement bin. This data represents the number of items (including duplicates) in the search result with a value for the given managed property that falls into this refinement bin.</span></span>  <br/>|
   

### <a name="example-refinement-data"></a><span data-ttu-id="d86ea-255">Пример: Данные уточнения</span><span class="sxs-lookup"><span data-stu-id="d86ea-255">Example: Refinement data</span></span>
<span data-ttu-id="d86ea-256"><a name="SP15_Example_refinement_data"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-256"></span></span>

<span data-ttu-id="d86ea-p132">В представленной ниже таблице 3 содержит две строки данных уточнения. Первая строка уточнения для сохранения данных индексированных элементов которой параметр тип файла имеет HTML-код. Второй строке содержит уточнения результатов поиска, данные для индексированных элементов, где время последнего изменения из 2013/09/21 до 2013/09/22.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p132">Table 3 below contains two rows of refinement data. The first row holds refinement data for indexed items, where the file type is HTML. The second row holds refinement data for indexed items, where the last modified time is from 2013/09/21 until 2013/09/22.</span></span>
  
    
    

<span data-ttu-id="d86ea-260">**В таблице 3: Формат и содержимое данных уточнения**</span><span class="sxs-lookup"><span data-stu-id="d86ea-260">**Table 3: Format and contents of refinement data**</span></span>


|<span data-ttu-id="d86ea-261">**RefinerName**</span><span class="sxs-lookup"><span data-stu-id="d86ea-261">**RefinerName**</span></span>|<span data-ttu-id="d86ea-262">**RefinementName**</span><span class="sxs-lookup"><span data-stu-id="d86ea-262">**RefinementName**</span></span>|<span data-ttu-id="d86ea-263">**RefinementValue**</span><span class="sxs-lookup"><span data-stu-id="d86ea-263">**RefinementValue**</span></span>|<span data-ttu-id="d86ea-264">**RefinementToken**</span><span class="sxs-lookup"><span data-stu-id="d86ea-264">**RefinementToken**</span></span>|<span data-ttu-id="d86ea-265">**RefinementCount**</span><span class="sxs-lookup"><span data-stu-id="d86ea-265">**RefinementCount**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d86ea-266">FileType</span><span class="sxs-lookup"><span data-stu-id="d86ea-266">FileType</span></span>  <br/>|<span data-ttu-id="d86ea-267">Html</span><span class="sxs-lookup"><span data-stu-id="d86ea-267">Html</span></span>  <br/>|<span data-ttu-id="d86ea-268">Html</span><span class="sxs-lookup"><span data-stu-id="d86ea-268">Html</span></span>  <br/>|<span data-ttu-id="d86ea-269">"???? 68746d6c»</span><span class="sxs-lookup"><span data-stu-id="d86ea-269">"????68746d6c"</span></span>  <br/>|<span data-ttu-id="d86ea-270">50553</span><span class="sxs-lookup"><span data-stu-id="d86ea-270">50553</span></span>  <br/>|
|<span data-ttu-id="d86ea-271">запись;</span><span class="sxs-lookup"><span data-stu-id="d86ea-271">Write</span></span>  <br/>|<span data-ttu-id="d86ea-272">Из 2013-09-21T00:00:00Z до 2013-09-22T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="d86ea-272">From 2013-09-21T00:00:00Z up to 2013-09-22T00:00:00Z</span></span>  <br/>|<span data-ttu-id="d86ea-273">Из 2013-09-21T00:00:00Z до 2013-09-22T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="d86ea-273">From 2013-09-21T00:00:00Z up to 2013-09-22T00:00:00Z</span></span>  <br/>|<span data-ttu-id="d86ea-274">диапазон (2013-09-21T00:00:00Z 2013-09-22T00:00:00Z)</span><span class="sxs-lookup"><span data-stu-id="d86ea-274">range(2013-09-21T00:00:00Z, 2013-09-22T00:00:00Z)</span></span>  <br/>|<span data-ttu-id="d86ea-275">37</span><span class="sxs-lookup"><span data-stu-id="d86ea-275">37</span></span>  <br/>|
   

## <a name="creating-a-refined-query"></a><span data-ttu-id="d86ea-276">Создание уточненного запроса</span><span class="sxs-lookup"><span data-stu-id="d86ea-276">Creating a refined query</span></span>
<span data-ttu-id="d86ea-277"><a name="SP15_Creating_refined_query"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-277"></span></span>

<span data-ttu-id="d86ea-p133">Результат поиска представляет параметры уточнения результатов поиска в виде строковые значения или диапазоны значений. Каждый строковое значение или числовое значение диапазона называется контейнера уточненияи каждой корзины уточнения имеет значение связанного **RefinementToken**. Параметр уточнения связан с управляемым свойством, предоставляемый значение **RefinerName**.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p133">A search result presents refinement options in the form of string values or value ranges. Each string value or numeric value range is called a refinement bin, and each refinement bin has an associated **RefinementToken** value. A refinement option is associated with a managed property, which is provided by the **RefinerName** value.</span></span>
  
    
    
<span data-ttu-id="d86ea-p134">Как **RefinementToken**, так и **RefinerName** значения объединяются для создания _refinement filter_ строки. Эта строка представляет фильтр, который можно использовать для ограничения элементов результатов поиска для включения только элементы которых управляемого свойства имеет значение внутри контейнера уточнения. В short:</span><span class="sxs-lookup"><span data-stu-id="d86ea-p134">Both the **RefinementToken** and **RefinerName** values are concatenated to create a _refinement filter_ string. This string represents a filter that can be used to limit search result items to include only items where a managed property has a value within a refinement bin. In short:</span></span>
  
    
    
 `refinement filter = <RefinerName>:<RefinementToken>`
  
    
    
<span data-ttu-id="d86ea-p135">Уточняющие фильтры для уточненного запроса можно обеспечить путем добавления фильтров уточнения свойство  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) класса [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) . Несколько фильтров уточнения позволяют предоставьте многоуровневой перехода в результатах поиска, для применения уточнения на многозначные свойства. Например можно уточнить запрос для элементов, которые имеют два автора - каждый из которых представлен контейнера уточнения -, но исключить элементы, которые имеют только один из авторов.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p135">You can provide one or more refinement filters for a refined query by adding refinement filters to the  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) class. Multiple refinement filters enable you to provide multilevel drill-down into the search results, and to apply refinement on multivalued properties. For example, you can refine the query to items that have two authors - each represented by a refinement bin - but exclude items that have only one of the authors.</span></span>
  
    
    

### <a name="example-1-creating-a-refined-query-for-html-file-types"></a><span data-ttu-id="d86ea-287">В примере 1: Создание уточненного запроса для типов файлов HTML</span><span class="sxs-lookup"><span data-stu-id="d86ea-287">Example 1: Creating a refined query for HTML file types</span></span>

<span data-ttu-id="d86ea-288">В следующем примере CSOM показано, как для программного выполнения уточнения результатов поиска, чтобы ограничить поиск теми только тип файла HTML.</span><span class="sxs-lookup"><span data-stu-id="d86ea-288">The following CSOM example shows how to programmatically perform a refinement, to limit the search results to those of HTML file type only.</span></span> <span data-ttu-id="d86ea-289">Как уже упоминалось в [Пример: данные уточнения](#SP15_Example_refinement_data), данных уточнения, связанных с этим параметром уточнения имеет **RefinerName** задать _Тип файла_ и **RefinementToken** присвоено значение _«????68746d6c»_.</span><span class="sxs-lookup"><span data-stu-id="d86ea-289">As mentioned in  [Example: Refinement data](#SP15_Example_refinement_data), refinement data related to this refinement option has **RefinerName** set to _Filetype_ and **RefinementToken** set to _"????68746d6c"_.</span></span>
  
    
    

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


### <a name="example-2-creating-a-refined-query-by-using-previously-obtained-refinement-data"></a><span data-ttu-id="d86ea-290">Пример 2: Создание уточненного запроса с помощью ранее полученные данные уточнения</span><span class="sxs-lookup"><span data-stu-id="d86ea-290">Example 2: Creating a refined query by using previously obtained refinement data</span></span>

<span data-ttu-id="d86ea-p137">В следующем примере CSOM показано, как выполнить запрос с помощью спецификации уточнения для создания данных уточнения, который впоследствии используется для выполнения уточнения результатов поиска. В этом примере моделирует процесс конечный пользователь при выборе первого параметра уточнения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="d86ea-p137">The following CSOM example shows how to run a query with a refiner spec to create refinement data which is subsequently used to perform refinement. This example simulates the process of an end user selecting the first refinement option.</span></span>
  
    
    

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
        var firstRefinementOption = refinementOptionArray[6];x
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


## <a name="see-also"></a><span data-ttu-id="d86ea-293">См. также</span><span class="sxs-lookup"><span data-stu-id="d86ea-293">See also</span></span>
<span data-ttu-id="d86ea-294"><a name="SP15_Query_refinement_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-294"></span></span>


-  [<span data-ttu-id="d86ea-295">Настройка свойств веб-части уточнения результатов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d86ea-295">Configure properties of the Refinement Web Part in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/gg549985.aspx)
    
  
-  [<span data-ttu-id="d86ea-296">Обзор схемы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d86ea-296">Overview of the search schema in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/jj219669%28office.15%29.aspx)
    
  

## <a name="see-also"></a><span data-ttu-id="d86ea-297">См. также</span><span class="sxs-lookup"><span data-stu-id="d86ea-297">See also</span></span>
<span data-ttu-id="d86ea-298"><a name="SP15_Query_refinement_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d86ea-298"></span></span>


#### <a name="other-resources"></a><span data-ttu-id="d86ea-299">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="d86ea-299">Other resources</span></span>


  
    
    
 [<span data-ttu-id="d86ea-300">Схема индекса (FAST Search Server для SharePoint)</span><span class="sxs-lookup"><span data-stu-id="d86ea-300">Index Schema (FAST Search Server 2010 for SharePoint)</span></span>](http://msdn.microsoft.com/library/3e1eed3f-8a6f-4911-9607-f1616e6a44f3%28Office.15%29.aspx)
  
    
    
 [<span data-ttu-id="d86ea-301">Элемент Refiner в схеме Microsoft.Search.Query</span><span class="sxs-lookup"><span data-stu-id="d86ea-301">Refiner Element in Microsoft.Search.Query Schema</span></span>](http://msdn.microsoft.com/library/0512c17a-18e9-45e3-9061-9dba9cd45ef4%28Office.15%29.aspx)
