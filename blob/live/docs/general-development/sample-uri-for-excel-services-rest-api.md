---
title: "Пример URI для интерфейса API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4ebe1da2-9861-416f-bef1-4a62599efe2e
ms.openlocfilehash: 003f7097ee68e014f232b3e4817ab397202675d0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sample-uri-for-excel-services-rest-api"></a><span data-ttu-id="35fe2-102">Пример URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="35fe2-102">Sample URI For Excel Services REST API</span></span>

<span data-ttu-id="35fe2-103">В этом разделе приведены примеры коды URI для команды службы передачи (REST) представлений состояний в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="35fe2-103">This topic lists sample URIs for the representational state transfer (REST) service commands in Excel Services.</span></span>
  
    
    


> <span data-ttu-id="35fe2-104">**Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="35fe2-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="35fe2-105">Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="35fe2-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="sample-uri-for-rest-commands-in-excel-services"></a><span data-ttu-id="35fe2-106">Пример URI для команды REST в службах Excel</span><span class="sxs-lookup"><span data-stu-id="35fe2-106">Sample URI for REST Commands in Excel Services</span></span>

<span data-ttu-id="35fe2-107">В следующих примерах каждый из URI ссылается на книгу с именем  *sampleWorkbook.xlsx*  .</span><span class="sxs-lookup"><span data-stu-id="35fe2-107">In the following examples, each URI references a workbook named  *sampleWorkbook.xlsx*  .</span></span>
  
    
    

- <span data-ttu-id="35fe2-108">Файл sampleWorkbook.xlsx содержит именованные диапазоны и диаграммы.</span><span class="sxs-lookup"><span data-stu-id="35fe2-108">The sampleWorkbook.xlsx file contains named ranges and charts.</span></span>
    
  
- <span data-ttu-id="35fe2-p102">Файл sampleWorkbook.xlsx сохраняется в надежной библиотеке документов SharePoint. В этом примере  это путь к папке sampleWorkbook.xlsx:</span><span class="sxs-lookup"><span data-stu-id="35fe2-p102">The sampleWorkbook.xlsx file is saved to a trusted SharePoint document library. In this example, the path to the location of sampleWorkbook.xlsx is:</span></span>
    
```
  
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```


### <a name="sample-uri"></a><span data-ttu-id="35fe2-111">Пример URI</span><span class="sxs-lookup"><span data-stu-id="35fe2-111">Sample URI</span></span>

<span data-ttu-id="35fe2-112">На странице ASPX для службы REST в Службы Excel  это:</span><span class="sxs-lookup"><span data-stu-id="35fe2-112">The .aspx page for the REST service in Excel Services is:</span></span> 
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx

```

<span data-ttu-id="35fe2-113">Ниже приведены коды URI для получения доступа к книгам sampleWorkbook.xlsx с помощью службы REST в Службы Excel примере.</span><span class="sxs-lookup"><span data-stu-id="35fe2-113">The following are example URIs to access the sampleWorkbook.xlsx workbook by using the REST service in Excel Services.</span></span> 
  
    
    

- <span data-ttu-id="35fe2-114">Модель верхнего уровня для книги (только диапазонов и диаграмм в текущем построении):</span><span class="sxs-lookup"><span data-stu-id="35fe2-114">Top-level model for the workbook (only ranges and charts in the current build):</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model

```

- <span data-ttu-id="35fe2-115">Получение полного книги:</span><span class="sxs-lookup"><span data-stu-id="35fe2-115">Get the full workbook:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=workbook

```

- <span data-ttu-id="35fe2-p103">Возвращает диапазон (по умолчанию html). Следующие два примера URI эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="35fe2-p103">Return a range (default html). The following two URI examples are equivalent:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')

```


```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?$format=html
```

- <span data-ttu-id="35fe2-118">Получение именованный диапазон:</span><span class="sxs-lookup"><span data-stu-id="35fe2-118">Get a named range:</span></span>
    
```
  http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('nameOfTheNamedRange')

```

- <span data-ttu-id="35fe2-119">Возвращать канал Atom XML:</span><span class="sxs-lookup"><span data-stu-id="35fe2-119">Return an Atom XML feed:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=atom

```

- <span data-ttu-id="35fe2-120">Задайте ячейки и вернуть его.</span><span class="sxs-lookup"><span data-stu-id="35fe2-120">Set a cell and return it:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?Ranges('Sheet1!C3')=demo

```

- <span data-ttu-id="35fe2-121">Получение диаграммы:</span><span class="sxs-lookup"><span data-stu-id="35fe2-121">Get a chart:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```

- <span data-ttu-id="35fe2-122">Задайте значение и получить диаграммы:</span><span class="sxs-lookup"><span data-stu-id="35fe2-122">Set a value and get a chart:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?Ranges('Sheet1!A1')=5.5

```

