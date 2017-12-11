---
title: "Запрашивает данные книги Excel с SharePoint Server с помощью OData"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f846e96-6c9e-4ed2-9602-4081ad0ab135
ms.openlocfilehash: c7547b4bc0b504780609dffafe7fc15669cd68c4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="requesting-excel-workbook-data-from-sharepoint-server-using-odata"></a>Запрашивает данные книги Excel с SharePoint Server с помощью OData

> [!NOTE]
> API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для учетных записей Office 365 для образования, Office 365 бизнес и Office 365 корпоративный используйте REST API Excel, входящие в состав конечной точки [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel).
  
    
    

URL-адреса использует OData для запроса сведений из ресурса. URL-адрес создавать определенным образом, используя параметры запроса, чтобы возвратить сведения, которые вы запрашиваете. Следующий URL-адрес показано, как выглядит типичное запросов OData. http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$top=20
  
    
    

Таким образом, чтобы он получает первых 20 строк в таблице с именем Table1 в книге ProductSales.xlsx, которая хранится в папку «документы» на сервере contoso1 структурирован этого примера запроса OData. URL-адрес использует параметр запроса система **$top** чтобы указать количество возвращаемых строк.Глядя близко URL-адрес, могут видеть его структуры три части: служба корневой URI; путь к ресурсу; и параметры запроса.
## <a name="service-root-uri"></a>Корень URI службы

Начальной части URL-адреса называется корневой службы и остаются неизменными для каждого запроса OData, вносимые в SharePoint server за исключением имени сервера. Он содержит имя сервера SharePoint, где хранится книга и путь, _vti_bin/ExcelRest.aspx, как показано в следующем примере.
  
    
    
http://contoso1/_vti_bin/ExcelRest.aspx
  
    
    

## <a name="resource-path"></a>Путь к ресурсу

Вторая часть URL-адрес имеет путь к книге Excel и указывает, что это запроса OData.
  
    
    
/Documents/ProductSales.xlsx/OData
  
    
    

## <a name="system-query-options"></a>Системные параметры запросов

Третья часть URL-адреса дает система параметров запросов для запроса. Параметры запроса всегда начинаются с символа доллара ($) и добавляются в конец URI как параметры запроса. В этом примере для первых 20 строк в таблице с именем Table1  запрос.
  
    
    
/ Table1? $top = 20
  
    
    
Системные параметры запросов позволяют получить данные из ресурса. Реализация OData служб Excel поддерживает ряд параметров запроса, перечисленные в следующем разделе.
  
    
    

## <a name="system-query-options"></a>Системные параметры запросов
<a name="xlsSystemQueryOptions"> </a>

Реализация служб Excel OData поддерживает ряд стандартные параметры запроса OData система. Эти параметры запроса являются основой запросов OData с момента параметры используются для указания, какие данные требуется получить из ресурса. В следующей таблице приведены параметры запросов системы, реализация службами Excel OData в настоящее время поддерживает.
  
    
    

**В таблице 1. Системные параметры запросов OData служб Excel**


|**Системный параметр запроса**|**Описание**|
|:-----|:-----|
|/\<tableName\>  <br/> |Возвращает все строки в таблице, указанный с \<tableName\>, где \<tableName\> — это имя таблицы в книгу Excel, которая содержит строки, которую необходимо получить.  <br/> **Важные:** Эта форма запроса OData возвращает не более 500 строк за раз. Каждый набор строк, 500 состоит из одной страницы. Для получения строк в дальнейшем страниц в таблице, имеющей более 500 строк, используйте параметр запроса **$skiptoken** (см. ниже).<br/>Следующий пример возвращает все строки до 500th строк в Table1 ProductSales.xlsx книги.  <br/> |
|**$metadata** <br/> |Возвращает все доступные таблицы и сведения о типе для всех строк в каждой таблице в указанной книге.  <br/> Следующий пример возвращает таблиц и сведения о типе для таблиц в книге ProductSales.xlsx.  <br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/$ метаданных  <br/> |
|**$orderby** <br/> |Возвращает строк в указанной таблице, отсортированные по значения, указанного в **$orderby**.  <br/> Следующий пример возвращает все строки в таблице 1, отсортированные по столбце имя в книге ProductSales.xlsx.  <br/> **Примечание**: по возрастанию значение по умолчанию для **$orderby** .          http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$ orderby = имя  <br/> |
|**$top** <br/> |Возвращает N строк из таблицы, где N  число указанное значение **$top**.  <br/> Следующий пример возвращает первые 5 строк из Table1, отсортированные по имени столбца в книге ProductSales.xlsx.  <br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1_qM _ $orderby = имя&amp;$top = 5  <br/> |
|**$skip** <br/> |Пропускает N строк, N  номер, указанный по значению **$skip**и затем возвращает остальных строк таблицы.  <br/> Следующий пример возвращает все оставшиеся строки после пятой из Table1 ProductSales.xlsx книги.  <br/> Пропустить $ http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1? = 5  <br/> |
|**$skiptoken** <br/> |Операций поиска n-й строке, где N  это положение строки порядковый номер, указанный в параметре значение **$skiptoken**и затем возвращает всех оставшихся строк, начиная с строки N + 1. Коллекция начинается с нуля, поэтому второй строке, например, обозначается $skiptoken = 1.<br/> Следующий пример возвращает все оставшиеся строки после второй строке из Table1 ProductSales.xlsx книги.  <br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$ skiptoken = 1  <br/> Можно также использовать параметр запроса **$skiptoken** для получения строк в страницы после первой страницы из таблицы, содержащее более 500 строк. Следующем примере показано, как получить строку 500th и более поздних версий, из таблицы с более чем 500 строк.<br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$ skiptoken = 499  <br/> |
|**$filter** <br/> |Возвращает набор строк, которые удовлетворяют условиям, указанным в значении **$filter**. Дополнительные сведения об операторах и набор функций, которые можно использовать с **$filter**OData  [документации](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)см. <br/> Следующий пример возвращает только строки, где значение столбца Price больше 100.  <br/> Фильтр $ http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1? = цена gt 100  <br/> |
|**$format** <br/> |Формат Atom XML поддерживается только значение и используется по умолчанию для параметра **$format** запрос. <br/> |
|**$select** <br/> |Возвращает сущности, указанной атрибутом **$select**.  <br/> Следующий пример выбирает в столбце имя из Table1 в книге ProductSales.xlsx.  <br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$ select = имя  <br/> |
|**$inlinecount** <br/> | Возвращает количество строк в указанной таблице. <br/>  $ **inlinecount** можно использовать только 1 из 2 из следующих значений. <br/><ul><li>**allpages**  возвращает количество для всех строк в таблице.</li><li>**none** - не включает число строк в таблице.</li></ul><br/>В следующем примере возвращается количество для общее число строк в Table1 в книге ProductSales.xlsx. <br/>  http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$ inlinecount = allpages <br/> |
   

## <a name="see-also"></a>См. также
<a name="xlsAdditionalResources"> </a>


-  [С помощью OData с помощью служб Excel REST в SharePoint](using-odata-with-excel-services-rest-in-sharepoint.md)
    
  
-  [Новые возможности служб Excel для разработчиков](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [Документация по спецификации OData](http://www.odata.org)
    
  
