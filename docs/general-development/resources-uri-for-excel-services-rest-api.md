---
title: "Ресурсы URI для интерфейса API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 79f95305-ec9e-4842-b937-85f66ced98e4
ms.openlocfilehash: 01b264b2e668e3779df8fcc08c70142241f7f8db
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="resources-uri-for-excel-services-rest-api"></a><span data-ttu-id="ccc11-102">Ресурсы URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="ccc11-102">Resources URI for Excel Services REST API</span></span>

<span data-ttu-id="ccc11-103">Непосредственно с помощью API-Интерфейс REST в Службы Excel можно связать сущности.</span><span class="sxs-lookup"><span data-stu-id="ccc11-103">You can link to entities directly by using the REST API in Excel Services.</span></span>
  
    
    


> <span data-ttu-id="ccc11-104">**Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="ccc11-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="ccc11-105">Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/ru-ru/docs/api-reference/v1.0/resources/excel
> ) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ccc11-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/ru-ru/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="base-rest-url"></a><span data-ttu-id="ccc11-106">URL-адрес базовый REST</span><span class="sxs-lookup"><span data-stu-id="ccc11-106">Base REST URL</span></span>

<span data-ttu-id="ccc11-107">Ниже приведен пример URL-адреса REST конкретного элемента в книге.</span><span class="sxs-lookup"><span data-stu-id="ccc11-107">The following is an example of a REST URL to a specific element in a workbook.</span></span>
  
    
    

```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

<span data-ttu-id="ccc11-p102">Относительный URL-адрес REST зависит от базовый URL-адрес REST. Ниже приведен пример базовый URL-адрес REST для конкретной книги.</span><span class="sxs-lookup"><span data-stu-id="ccc11-p102">A relative REST URL is based off the base REST URL. The following is an example of a base REST URL to a specific workbook.</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>
```

<span data-ttu-id="ccc11-110">Например, если у вас есть книгу с именем «sampleWorkbook.xlsx» в библиотеке документов, следующие:</span><span class="sxs-lookup"><span data-stu-id="ccc11-110">For example, if you have a workbook named "sampleWorkbook.xlsx" in the following document library:</span></span> 
  
    
    



```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

<span data-ttu-id="ccc11-111"> Это базовый URL-адрес REST в книге:</span><span class="sxs-lookup"><span data-stu-id="ccc11-111">The base REST URL to the workbook is:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx
```


## <a name="resources-uri"></a><span data-ttu-id="ccc11-112">URI-код ресурсов</span><span class="sxs-lookup"><span data-stu-id="ccc11-112">Resources URI</span></span>

<span data-ttu-id="ccc11-p103">В таблице 1 приведены всех доступных ресурсах в Службы Excel API-интерфейса REST. Для доступа к определенному ресурсу, добавьте расположение ресурсов базовый URL-адрес REST в книгу.</span><span class="sxs-lookup"><span data-stu-id="ccc11-p103">Table 1 shows all the accessible resources in the Excel Services REST API. To access a particular resource, append the resource location to the base REST URL to a workbook.</span></span>
  
    
    

<span data-ttu-id="ccc11-115">**В таблице 1. Ресурсы, доступных в API REST служб Excel**</span><span class="sxs-lookup"><span data-stu-id="ccc11-115">**Table 1. Accessible resources in the Excel Services REST API**</span></span>


|<span data-ttu-id="ccc11-116">**Расположение ресурсов**</span><span class="sxs-lookup"><span data-stu-id="ccc11-116">**Resource Location**</span></span>|<span data-ttu-id="ccc11-117">**Формат**</span><span class="sxs-lookup"><span data-stu-id="ccc11-117">**Format**</span></span>|<span data-ttu-id="ccc11-118">**Пример**</span><span class="sxs-lookup"><span data-stu-id="ccc11-118">**Example**</span></span>|<span data-ttu-id="ccc11-119">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccc11-119">**Notes**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="ccc11-120">/ модель</span><span class="sxs-lookup"><span data-stu-id="ccc11-120">/model</span></span>  <br/> |<span data-ttu-id="ccc11-121">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-121">Atom (default)</span></span>  <br/> |<span data-ttu-id="ccc11-122">/ модель</span><span class="sxs-lookup"><span data-stu-id="ccc11-122">/model</span></span>  <br/> |<span data-ttu-id="ccc11-p104">Возвращает канала с ресурсами, поддерживаемый Службы Excel API-Интерфейс REST Atom. Поддерживаемые ресурсы, диапазоны, диаграмм, таблиц и сводных таблиц.</span><span class="sxs-lookup"><span data-stu-id="ccc11-p104">Returns an Atom feed with the resources supported by the Excel Services REST API. The supported resources are ranges, charts, tables, and PivotTables.</span></span>  <br/> |
|<span data-ttu-id="ccc11-125">аудио- и модель</span><span class="sxs-lookup"><span data-stu-id="ccc11-125">/model</span></span>  <br/> |<span data-ttu-id="ccc11-126">workbook</span><span class="sxs-lookup"><span data-stu-id="ccc11-126">workbook</span></span>  <br/> |<span data-ttu-id="ccc11-127">аудио- и модель? $format = книги</span><span class="sxs-lookup"><span data-stu-id="ccc11-127">/model?$format=workbook</span></span>  <br/> |<span data-ttu-id="ccc11-p105">Это рабочей книги. Поддерживаемые книги форматов, xlsx, xlsb и xlsm.</span><span class="sxs-lookup"><span data-stu-id="ccc11-p105">This is the workbook. Supported workbook formats are xlsx, xlsb, and xlsm.</span></span>  <br/> |
|<span data-ttu-id="ccc11-130">/ модели/диапазонов</span><span class="sxs-lookup"><span data-stu-id="ccc11-130">/model/Ranges</span></span>  <br/> |<span data-ttu-id="ccc11-131">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-131">Atom (default)</span></span>  <br/> |<span data-ttu-id="ccc11-132">Диапазоны/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-132">/model/Ranges?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-133">Веб-канала Atom, listis всех именованных диапазонов в книге.</span><span class="sxs-lookup"><span data-stu-id="ccc11-133">An Atom feed that listis all the named ranges in the workbook.</span></span>  <br/> |
|<span data-ttu-id="ccc11-134">/Model/Ranges('[name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-134">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-135">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-135">HTML (default)</span></span>  <br/> |<span data-ttu-id="ccc11-136">/model/Ranges('MyRange')?$format=html</span><span class="sxs-lookup"><span data-stu-id="ccc11-136">/model/Ranges('MyRange')?$format=html</span></span>  <br/> |<span data-ttu-id="ccc11-137">Фрагмент HTML-кода для запрошенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="ccc11-137">An HTML fragment for the requested range.</span></span>  <br/> |
|<span data-ttu-id="ccc11-138">/Model/Ranges('[name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-138">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-139">Atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-139">Atom</span></span>  <br/> |<span data-ttu-id="ccc11-140">/model/Ranges('MyRange')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-140">/model/Ranges('MyRange')?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-141">Запись Atom, содержащий XML-представление данных в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="ccc11-141">An Atom entry that contains an XML representation of the data within the range.</span></span>  <br/> |
|<span data-ttu-id="ccc11-142">/ модели/диаграмм</span><span class="sxs-lookup"><span data-stu-id="ccc11-142">/model/Charts</span></span>  <br/> |<span data-ttu-id="ccc11-143">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-143">Atom (default)</span></span>  <br/> |<span data-ttu-id="ccc11-144">Диаграммы/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-144">/model/Charts?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-145">Канала Atom, в котором приведены все диаграммы в книге.</span><span class="sxs-lookup"><span data-stu-id="ccc11-145">An Atom feed that lists all the charts in the workbook.</span></span>  <br/> |
|<span data-ttu-id="ccc11-146">/Model/Charts('[name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-146">/model/Charts('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-147">Изображение (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-147">Image (default)</span></span>  <br/> |<span data-ttu-id="ccc11-148">/model/Charts('MyChart')?$format=image</span><span class="sxs-lookup"><span data-stu-id="ccc11-148">/model/Charts('MyChart')?$format=image</span></span>  <br/> |<span data-ttu-id="ccc11-p106">Изображение диаграммы.  Это изображение в формате Portable Network Graphics (PNG).</span><span class="sxs-lookup"><span data-stu-id="ccc11-p106">An image of the chart. The image is in Portable Network Graphics (PNG) format.</span></span>  <br/> |
|<span data-ttu-id="ccc11-151">/ модели/таблиц</span><span class="sxs-lookup"><span data-stu-id="ccc11-151">/model/Tables</span></span>  <br/> |<span data-ttu-id="ccc11-152">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-152">Atom (default)</span></span>  <br/> |<span data-ttu-id="ccc11-153">Таблицы/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-153">/model/Tables?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-154">Канала Atom, который перечисляет все таблицы, доступные в книге.</span><span class="sxs-lookup"><span data-stu-id="ccc11-154">An Atom feed that lists all the available tables in the workbook.</span></span>  <br/> |
|<span data-ttu-id="ccc11-155">/Model/Tables('[name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-155">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-156">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-156">HTML (default)</span></span>  <br/> |<span data-ttu-id="ccc11-157">/model/Tables('MyTable')?$format=html</span><span class="sxs-lookup"><span data-stu-id="ccc11-157">/model/Tables('MyTable')?$format=html</span></span>  <br/> |<span data-ttu-id="ccc11-158">Фрагмент HTML-кода для запрошенного таблицы.</span><span class="sxs-lookup"><span data-stu-id="ccc11-158">An HTML fragment for the requested table.</span></span>  <br/> |
|<span data-ttu-id="ccc11-159">/Model/Tables('[name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-159">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-160">Atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-160">Atom</span></span>  <br/> |<span data-ttu-id="ccc11-161">/model/Tables('MyTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-161">/model/Tables('MyTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-162">Запись Atom, содержащий XML-представление данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="ccc11-162">An Atom entry that contains an XML representation of the data within the table.</span></span>  <br/> |
|<span data-ttu-id="ccc11-163">/model/PivotTables</span><span class="sxs-lookup"><span data-stu-id="ccc11-163">/model/PivotTables</span></span>  <br/> |<span data-ttu-id="ccc11-164">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-164">Atom (default)</span></span>  <br/> |<span data-ttu-id="ccc11-165">/model/PivotTables?$format=atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-165">/model/PivotTables?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-166">Канала Atom, в котором приведены все доступные сводных таблиц в книге</span><span class="sxs-lookup"><span data-stu-id="ccc11-166">An Atom feed that lists all the available PivotTables in the workbook</span></span>  <br/> |
|<span data-ttu-id="ccc11-167">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-167">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-168">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ccc11-168">HTML (default)</span></span>  <br/> |<span data-ttu-id="ccc11-169">/model/PivotTables('MyPivotTable)?$format=html</span><span class="sxs-lookup"><span data-stu-id="ccc11-169">/model/PivotTables('MyPivotTable)?$format=html</span></span>  <br/> |<span data-ttu-id="ccc11-170">Фрагмент HTML-кода для запрошенного сводных таблиц.</span><span class="sxs-lookup"><span data-stu-id="ccc11-170">An HTML fragment for the requested PivotTable.</span></span>  <br/> |
|<span data-ttu-id="ccc11-171">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="ccc11-171">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="ccc11-172">Atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-172">Atom</span></span>  <br/> |<span data-ttu-id="ccc11-173">/model/PivotTables('MyPivotTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="ccc11-173">/model/PivotTables('MyPivotTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="ccc11-174">Запись Atom, содержащий XML-представление данных в сводных таблицах.</span><span class="sxs-lookup"><span data-stu-id="ccc11-174">An Atom entry that contains an XML representation of the data within the PivotTables.</span></span>  <br/> |
   

> <span data-ttu-id="ccc11-175">**Примечание:** Службы Excel — ограничивает число диапазоны, которые можно включить в URL-адреса до 10.</span><span class="sxs-lookup"><span data-stu-id="ccc11-175">**Note:** Excel Services limits the number of ranges that you can include in a URL to 10.</span></span> <span data-ttu-id="ccc11-176">Если включить более 10 диапазоны в URL-адрес, вы получите сообщение о том, что служба недоступна.</span><span class="sxs-lookup"><span data-stu-id="ccc11-176">If you include more than 10 Ranges in a URL, you will get an error that indicates that the service is unavailable.</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="ccc11-177">См. также</span><span class="sxs-lookup"><span data-stu-id="ccc11-177">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="ccc11-178">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="ccc11-178">Concepts</span></span>


  
    
    
 [<span data-ttu-id="ccc11-179">Структура базового URI и путь</span><span class="sxs-lookup"><span data-stu-id="ccc11-179">Basic URI Structure and Path</span></span>](basic-uri-structure-and-path.md)
