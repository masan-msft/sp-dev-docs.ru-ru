---
title: "Структура базового URI и путь"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d73cf6c2-0677-4726-8a3e-2ad130e1a12c
ms.openlocfilehash: 2902dca96c5325250d8e1cd31647172e6968d632
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="basic-uri-structure-and-path"></a><span data-ttu-id="ed8c5-102">Структура базового URI и путь</span><span class="sxs-lookup"><span data-stu-id="ed8c5-102">Basic URI Structure and Path</span></span>

<span data-ttu-id="ed8c5-103">В этом разделе объясняется, как создать URI структуры и путь для команды службы REST в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-103">This topic explains how to construct the URI structure and path for REST service commands in Excel Services.</span></span>
  
    
    


> <span data-ttu-id="ed8c5-104">**Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="ed8c5-105">Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="basic-url-structure-and-path"></a><span data-ttu-id="ed8c5-106">Структура базового URL-адреса и пути</span><span class="sxs-lookup"><span data-stu-id="ed8c5-106">Basic URL Structure and Path</span></span>

<span data-ttu-id="ed8c5-p102">API-Интерфейс REST в Службы Excel дает возможность получить доступ к ресурсам как диаграммы, сводные таблицы, таблиц и именованных диапазонов в книге непосредственно через URL-адрес. Каждый URL-адрес REST в Службы Excel построения из трех частей. Ниже представлена базовая структура URL-адреса для доступа к ресурсам в книге:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p102">The REST API in Excel Services gives you the ability to access resources like charts, PivotTables, tables, and named ranges in a workbook directly through a URL. Each REST URL in Excel Services is built of three parts. Following is the basic structure of the URL to access the resources in a workbook:</span></span> 
  
    
    

1. <span data-ttu-id="ed8c5-110">**REST aspx URI страницы** Точка входа в страницу ASPX</span><span class="sxs-lookup"><span data-stu-id="ed8c5-110">**REST aspx Page URI** The entry point to an .aspx page</span></span>
    
  
2. <span data-ttu-id="ed8c5-111">**Расположение книги** Путь к книге</span><span class="sxs-lookup"><span data-stu-id="ed8c5-111">**Workbook Location** The path to the workbook</span></span>
    
  
3. <span data-ttu-id="ed8c5-112">**Расположение ресурсов** Путь к запрошенному ресурсу внутри книги</span><span class="sxs-lookup"><span data-stu-id="ed8c5-112">**Resource Location** The path to the requested resource inside the workbook</span></span>
    
  
<span data-ttu-id="ed8c5-113">Ниже приведен пример URL-адреса REST конкретного элемента в книге:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-113">Following is the construct for the REST URL to a specific element in a workbook:</span></span>
  
    
    



```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

<span data-ttu-id="ed8c5-p103">Ниже приведен пример вид URL-адреса REST в Службы Excel все три части в сочетании. В этом примере URL-адреса REST обращается к книги с названием «sampleWorkbook.xlsx», который содержит диаграммы, называется «SampleChart»:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p103">Following is an example of how a REST URL in Excel Services looks with all three parts combined. In this example, the REST URL is accessing a workbook called "sampleWorkbook.xlsx" that contains a chart called "SampleChart":</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart')
```

<span data-ttu-id="ed8c5-p104">Книга хранится в библиотеке документов. Полный путь к книге  _<ServerName>_ `http://` `/Docs/Documents/sampleWorkbook.xlsx`.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p104">The workbook is stored in a document library. The full path to the workbook is  `http://` _<ServerName>_ `/Docs/Documents/sampleWorkbook.xlsx`.</span></span>
  
    
    
<span data-ttu-id="ed8c5-118">Три части URL-адрес REST следующие:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-118">The three parts of the REST URL are:</span></span>
  
    
    

1. <span data-ttu-id="ed8c5-119">**REST aspx URI страницы**: _<ServerName>_ `http://` `/_vti_bin/ExcelRest.aspx`</span><span class="sxs-lookup"><span data-stu-id="ed8c5-119">**REST aspx Page URI**: `http://` _<ServerName>_ `/_vti_bin/ExcelRest.aspx`</span></span>
    
  
2. <span data-ttu-id="ed8c5-120">**Расположение книги**: `/Docs/Documents/sampleWorkbook.xlsx`</span><span class="sxs-lookup"><span data-stu-id="ed8c5-120">**Workbook Location**: `/Docs/Documents/sampleWorkbook.xlsx`</span></span>
    
  
3. <span data-ttu-id="ed8c5-121">**Расположение ресурса**: `/model/Ranges('nameOfTheNamedRange')`</span><span class="sxs-lookup"><span data-stu-id="ed8c5-121">**Resource Location**: `/model/Ranges('nameOfTheNamedRange')`</span></span>
    
  

### <a name="accessing-by-using-the-discovery-user-interface"></a><span data-ttu-id="ed8c5-122">Доступ к с помощью пользовательского интерфейса обнаружения</span><span class="sxs-lookup"><span data-stu-id="ed8c5-122">Accessing by Using the Discovery User Interface</span></span>

<span data-ttu-id="ed8c5-p105">Можно также получить доступ к диаграмме с помощью пользовательского интерфейса обнаружения. Чтобы получить доступ к ресурсам как диаграммы, таблицы, сводные таблицы и диапазонов с помощью механизма обнаружения, показано на следующем снимке экрана, обратитесь к разделу  [Обнаружение в API REST служб Excel](discovery-in-excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p105">You can also access the chart by using the discovery user interface. To learn how access resources like charts, tables, PivotTables, and ranges by using the discovery mechanism shown in the following screen shot, see  [Discovery in Excel Services REST API](discovery-in-excel-services-rest-api.md).</span></span>
  
    
    

  
    
    
![URL-адрес модели REST служб Excel](../images/SharePointServer14Con_XLSvcs_RESTModel.gif)
  
    
    

  
    
    

  
    
    

  
    
    

### <a name="marker-path"></a><span data-ttu-id="ed8c5-126">Путь в маркер</span><span class="sxs-lookup"><span data-stu-id="ed8c5-126">Marker Path</span></span>

<span data-ttu-id="ed8c5-127">Ниже приведен на aspx-странице для службы REST в Службы Excel:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-127">Following is the aspx page for the REST service in Excel Services:</span></span>
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```

<span data-ttu-id="ed8c5-128">Для доступа к службе REST в Службы Excel, необходимо перед ввести URL-адрес с _<ServerName>_ `http://` `/_vti_bin/ExcelRest.aspx`.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-128">To access the REST service in Excel Services, you must preface the URL with  `http://` _<ServerName>_ `/_vti_bin/ExcelRest.aspx`.</span></span>
  
    
    

### <a name="workbook-location"></a><span data-ttu-id="ed8c5-129">Расположение книги</span><span class="sxs-lookup"><span data-stu-id="ed8c5-129">Workbook Location</span></span>

<span data-ttu-id="ed8c5-p106">Расположение книги  это относительный путь к книге, которая содержит ресурсы, которые нуждаются в доступе к. Например предположим, что у вас есть книгу с именем sampleWorkbook.xlsx, сохраненный на надежной библиотеки документов SharePoint. В этом примере следующие  это путь к папке sampleWorkbook.xlsx:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p106">The workbook location is the relative path to the workbook that has resources that you are interested in accessing. For example, assume that you have a workbook named sampleWorkbook.xlsx, saved to a trusted SharePoint document library. In this example, following is the path to the location of sampleWorkbook.xlsx:</span></span> 
  
    
    

```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

<span data-ttu-id="ed8c5-p107">Выполните относительный путь к книге ( `Docs/Documents/sampleWorkbook.xlsx`) и добавьте к пути маркер. Ниже приведен URL-адрес с добавленным расположением книгу и путь маркер.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p107">You take the relative path to the workbook ( `Docs/Documents/sampleWorkbook.xlsx`) and append it to the marker path. Following is the URL with the marker path and workbook location appended:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```


### <a name="resource-location"></a><span data-ttu-id="ed8c5-135">Расположение ресурсов</span><span class="sxs-lookup"><span data-stu-id="ed8c5-135">Resource Location</span></span>

<span data-ttu-id="ed8c5-p108">Расположение ресурсов  это путь внутри книги в элемент при запросе. Например если вы хотите получить диаграммы, расположение ресурсов будет выглядеть  `/model/Charts('Chart 1')`.</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p108">The resource location is the path inside the workbook to the element that you request. For example, if you want to get a chart, the resource location would be similar to  `/model/Charts('Chart 1')`.</span></span>
  
    
    
<span data-ttu-id="ed8c5-p109">Полный URL-адрес добавьте это маркер путь и относительный путь к книге. Ниже приведен полный пример URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="ed8c5-p109">For the full URL, you append this to the marker path and the relative path to the workbook. Following is the full example URL:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```


## <a name="see-also"></a><span data-ttu-id="ed8c5-140">См. также</span><span class="sxs-lookup"><span data-stu-id="ed8c5-140">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="ed8c5-141">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="ed8c5-141">Concepts</span></span>


  
    
    
 [<span data-ttu-id="ed8c5-142">Ресурсы URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="ed8c5-142">Resources URI for Excel Services REST API</span></span>](resources-uri-for-excel-services-rest-api.md)
  
    
    
 [<span data-ttu-id="ed8c5-143">Обнаружение в API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="ed8c5-143">Discovery in Excel Services REST API</span></span>](discovery-in-excel-services-rest-api.md)
