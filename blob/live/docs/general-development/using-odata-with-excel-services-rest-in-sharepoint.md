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
# <a name="using-odata-with-excel-services-rest-in-sharepoint"></a><span data-ttu-id="0e2ad-102">С помощью OData с помощью служб Excel REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e2ad-102">Using OData with Excel Services REST in SharePoint</span></span>
<span data-ttu-id="0e2ad-103">SharePoint Server 2010 появился API-Интерфейс REST для использования в считывание и запись сведений в книгах Excel, хранящиеся в библиотеках документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-103">SharePoint Server 2010 introduced the REST API for use in getting and setting information in Excel Workbooks stored in SharePoint document libraries.</span></span> <span data-ttu-id="0e2ad-104">SharePoint добавляет новый способ запроса данных из служб Excel, использующего Open Data Protocol (OData) которого можно использовать для получения сведений обо всех ресурсах служб Excel.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-104">SharePoint adds a new way to request data from Excel Services that uses the Open Data Protocol (OData) which you can use to get information about Excel Services resources.</span></span> <span data-ttu-id="0e2ad-105">Эта новая служба во многом зависит от существующего интерфейса API REST служб Excel. В этом разделе представлены высокоуровневый обзор использования OData в службах Excel.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-105">This new service relies heavily on the existing Excel Services REST API.This topic provides a high-level overview for using OData in Excel Services.</span></span>
> <span data-ttu-id="0e2ad-106">**Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-106">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="0e2ad-107">Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-107">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="what-is-odata"></a><span data-ttu-id="0e2ad-108">Что такое OData?</span><span class="sxs-lookup"><span data-stu-id="0e2ad-108">What is OData?</span></span>
<span data-ttu-id="0e2ad-109"><a name="xlsWhatIsOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-109"></span></span>

<span data-ttu-id="0e2ad-p103">OData является протоколом открыть веб-узел для запроса и изменения данных. Он используется RESTful подход для возврата данных ресурсы в Интернете. То есть использовать URI с помощью параметров запроса, включенные для получения сведений о определенного ресурса.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p103">OData is an open web protocol for querying and updating data. It uses a RESTful approach to return data from resources on the web. That is, you use a URI with query parameters included to get information about a specific resource.</span></span>
  
    
    
<span data-ttu-id="0e2ad-113">Дополнительные сведения о OData для  [спецификации Open Data Protocol](http://www.odata.org)см.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-113">For more information about OData, see the website for the  [Open Data Protocol specification](http://www.odata.org).</span></span>
  
    
    

## <a name="how-do-you-use-odata-with-excel-services"></a><span data-ttu-id="0e2ad-114">Как использовать OData со службами Excel</span><span class="sxs-lookup"><span data-stu-id="0e2ad-114">How do you use OData with Excel Services?</span></span>
<span data-ttu-id="0e2ad-115"><a name="xlsHowUseOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-115"></span></span>

<span data-ttu-id="0e2ad-p104">В случае Службы Excel использовать OData для получения сведений о таблиц (включая таблицы запросов) в книге, которая хранится в библиотеке SharePoint. Служба OData возвращает запрашиваемых в данных в формате XML Atom.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p104">In the case of Excel Services, you use OData to get information about tables (including query tables) in a workbook that is stored in a SharePoint library. The OData service returns the data that you requested in the in the XML Atom format.</span></span>
  
    
    

### <a name="syntax-for-making-odata-requests-to-excel-services"></a><span data-ttu-id="0e2ad-118">Синтаксис для выполнения запросов OData в службах Excel</span><span class="sxs-lookup"><span data-stu-id="0e2ad-118">Syntax for making OData requests to Excel Services</span></span>
<span data-ttu-id="0e2ad-119"><a name="xlsOdataSyntax"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-119"></span></span>

<span data-ttu-id="0e2ad-p105">SharePoint представляет каждой книге как отдельный ресурс, который можно запросить сведения из. В этом выпуске SharePoint Server вы можете получить данные из таблиц в книге.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p105">SharePoint exposes each workbook as a separate resource that you can request information from. In this release of SharePoint Server, you can only get data from tables in the workbook.</span></span>
  
    
    
<span data-ttu-id="0e2ad-p106">Для получения данных из книги Excel, создания URL-адрес, указывающий на книгу и, которое указывает, какие данные, чтобы получить из книги, а также упорядочить эти данные. Например чтобы получить сведения о Table1 в книгу с именем ProductSales.xlsx, которая хранится в библиотеке SharePoint в папку с именем документы, используется URL-адрес, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p106">To get data from an Excel workbook, you construct a URL that points to the workbook, and that specifies what data that you want to get from the workbook, and how to arrange that data. For example, to get information about Table1 in a workbook named ProductSales.xlsx that is stored on a SharePoint library in a folder that is named Documents, you would use a URL as follows.</span></span>
  
    
    
<span data-ttu-id="0e2ad-124">http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1</span><span class="sxs-lookup"><span data-stu-id="0e2ad-124">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1</span></span>
  
    
    
<span data-ttu-id="0e2ad-125">Дополнительные сведения о том, как использовать OData для запроса сведений из книги Excel, хранящихся на SharePoint Server можно  [Запрашивает данные книги Excel с SharePoint Server с помощью OData](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md).</span><span class="sxs-lookup"><span data-stu-id="0e2ad-125">For more information about how to use OData to request information from an Excel workbook stored on SharePoint Server, see  [Requesting Excel workbook data from SharePoint Server using OData](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md).</span></span>
  
    
    

## <a name="data-returned-by-odata"></a><span data-ttu-id="0e2ad-126">Данные, возвращаемые OData</span><span class="sxs-lookup"><span data-stu-id="0e2ad-126">Data returned by OData</span></span>
<span data-ttu-id="0e2ad-127"><a name="xlsOdataReturnData"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-127"></span></span>

<span data-ttu-id="0e2ad-p107">После выполнения запроса OData для Службы Excel, он возвращает XML в формате Atom. Формат Atom является единственным форматом, поддерживаемые в реализации Службы Excel OData. Например ниже показан запрос OData для первой строки в первой таблице (с именем Table1) в книгу с именем WindowsPhoneComparison.xlsx.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p107">When you make an OData request to Excel Services, it returns XML in the Atom format. The Atom format is the only supported format in the Excel Services implementation of OData. For example, the following shows an OData request for the first row in the first table (named Table1) in a workbook named WindowsPhoneComparison.xlsx.</span></span>
  
    
    
<span data-ttu-id="0e2ad-131">http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/odata/Table1</span><span class="sxs-lookup"><span data-stu-id="0e2ad-131">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/odata/Table1</span></span>
  
    
    
<span data-ttu-id="0e2ad-132">Службы Excel возвращает XML Atom, показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-132">Excel Services then returns the Atom XML shown in the following code.</span></span>
  
    
    



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


## <a name="conclusion"></a><span data-ttu-id="0e2ad-133">Заключение</span><span class="sxs-lookup"><span data-stu-id="0e2ad-133">Conclusion</span></span>
<span data-ttu-id="0e2ad-134"><a name="xlsOdataReturnData"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-134"></span></span>

<span data-ttu-id="0e2ad-p108">OData предоставляет простой способ получения данных из Excel книг, хранящихся на SharePoint. С помощью простого синтаксиса, на основе веб-стандартов, как HTTP и REST, OData позволяет быстро и легко получить данные из Excel книг.</span><span class="sxs-lookup"><span data-stu-id="0e2ad-p108">OData provides a simple way to get data from Excel workbooks that are stored on SharePoint. Using a straightforward syntax that is based on web standards like HTTP and REST, OData lets you quickly and easily get data from Excel workbooks.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="0e2ad-137">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0e2ad-137">Additional resources</span></span>
<span data-ttu-id="0e2ad-138"><a name="xlsOdataAddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="0e2ad-138"></span></span>


-  [<span data-ttu-id="0e2ad-139">Новые возможности служб Excel для разработчиков</span><span class="sxs-lookup"><span data-stu-id="0e2ad-139">What's new in Excel Services for developers</span></span>](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [<span data-ttu-id="0e2ad-140">Запрашивает данные книги Excel с SharePoint Server с помощью OData</span><span class="sxs-lookup"><span data-stu-id="0e2ad-140">Requesting Excel workbook data from SharePoint Server using OData</span></span>](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md)
    
  
-  [<span data-ttu-id="0e2ad-141">Документация по спецификации OData</span><span class="sxs-lookup"><span data-stu-id="0e2ad-141">OData specification documentation</span></span>](http://www.odata.org)
    
  

