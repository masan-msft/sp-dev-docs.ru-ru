---
title: "С помощью OData с помощью служб Excel REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8a20225a-323c-4420-bbb4-eef60aed4b42
ms.openlocfilehash: 61d8691d95786ed10a514d0c990b5ab61859faaf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="using-odata-with-excel-services-rest-in-sharepoint"></a>С помощью OData с помощью служб Excel REST в SharePoint
SharePoint Server 2010 появился API-Интерфейс REST для использования в считывание и запись сведений в книгах Excel, хранящиеся в библиотеках документов SharePoint. SharePoint добавляет новый способ запроса данных из служб Excel, использующего Open Data Protocol (OData) которого можно использовать для получения сведений обо всех ресурсах служб Excel. Эта новая служба во многом зависит от существующего интерфейса API REST служб Excel. В этом разделе представлены высокоуровневый обзор использования OData в службах Excel.
> **Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.
  
    
    


## <a name="what-is-odata"></a>Что такое OData?
<a name="xlsWhatIsOdata"> </a>

OData является протоколом открыть веб-узел для запроса и изменения данных. Он используется RESTful подход для возврата данных ресурсы в Интернете. То есть использовать URI с помощью параметров запроса, включенные для получения сведений о определенного ресурса.
  
    
    
Дополнительные сведения о OData для  [спецификации Open Data Protocol](http://www.odata.org)см.
  
    
    

## <a name="how-do-you-use-odata-with-excel-services"></a>Как использовать OData со службами Excel
<a name="xlsHowUseOdata"> </a>

В случае Службы Excel использовать OData для получения сведений о таблиц (включая таблицы запросов) в книге, которая хранится в библиотеке SharePoint. Служба OData возвращает запрашиваемых в данных в формате XML Atom.
  
    
    

### <a name="syntax-for-making-odata-requests-to-excel-services"></a>Синтаксис для выполнения запросов OData в службах Excel
<a name="xlsOdataSyntax"> </a>

SharePoint представляет каждой книге как отдельный ресурс, который можно запросить сведения из. В этом выпуске SharePoint Server вы можете получить данные из таблиц в книге.
  
    
    
Для получения данных из книги Excel, создания URL-адрес, указывающий на книгу и, которое указывает, какие данные, чтобы получить из книги, а также упорядочить эти данные. Например чтобы получить сведения о Table1 в книгу с именем ProductSales.xlsx, которая хранится в библиотеке SharePoint в папку с именем документы, используется URL-адрес, следующим образом.
  
    
    
http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1
  
    
    
Дополнительные сведения о том, как использовать OData для запроса сведений из книги Excel, хранящихся на SharePoint Server можно  [Запрашивает данные книги Excel с SharePoint Server с помощью OData](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md).
  
    
    

## <a name="data-returned-by-odata"></a>Данные, возвращаемые OData
<a name="xlsOdataReturnData"> </a>

После выполнения запроса OData для Службы Excel, он возвращает XML в формате Atom. Формат Atom является единственным форматом, поддерживаемые в реализации Службы Excel OData. Например ниже показан запрос OData для первой строки в первой таблице (с именем Table1) в книгу с именем WindowsPhoneComparison.xlsx.
  
    
    
http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/odata/Table1
  
    
    
Службы Excel возвращает XML Atom, показано в следующем коде.
  
    
    



```XML

<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<entry xml:base="http://{serverName}/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/OData" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:etag="W/&amp;quot;datetime'0001-01-01T00%3A00%3A00'&amp;quot;" xmlns="http://www.w3.org/2005/Atom">
  <id>http://{serverName}/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/OData/Table1(0)</id>
  <title type="text"></title>
  <updated>0001-01-01T00:00:00-08:00</updated>
  <author>
    <name />
  </author>
  <link rel="edit" title="Table1Item" href="/Table1(0)" />
  <category term="ExcelServices.Table1Item" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <content type="application/xml">
    <m:properties>
      <d:Phone>Samsung Focus</d:Phone>
      <d:sizeweight m:type="Edm.Double">4</d:sizeweight>
      <d:camera m:type="Edm.Double">2.5</d:camera>
      <d:battery m:type="Edm.Double">3</d:battery>
      <d:memory m:type="Edm.Double">3</d:memory>
      <d:speed m:type="Edm.Double">3</d:speed>
      <d:style m:type="Edm.Double">3</d:style>
      <d:callquality m:type="Edm.Double">3</d:callquality>
      <d:overall m:type="Edm.Double">3</d:overall>
      <d:excelRowID m:type="Edm.Int32">0</d:excelRowID>
    </m:properties>
  </content>
</entry>

```


## <a name="conclusion"></a>Заключение
<a name="xlsOdataReturnData"> </a>

OData предоставляет простой способ получения данных из Excel книг, хранящихся на SharePoint. С помощью простого синтаксиса, на основе веб-стандартов, как HTTP и REST, OData позволяет быстро и легко получить данные из Excel книг.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="xlsOdataAddRes"> </a>


-  [Новые возможности служб Excel для разработчиков](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [Запрашивает данные книги Excel с SharePoint Server с помощью OData](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md)
    
  
-  [Документация по спецификации OData](http://www.odata.org)
    
  

