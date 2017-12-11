---
title: "Ресурсы URI для интерфейса API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 79f95305-ec9e-4842-b937-85f66ced98e4
ms.openlocfilehash: e1b77373e293051315900e9fb06cb287c46e509e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="resources-uri-for-excel-services-rest-api"></a><span data-ttu-id="cba94-102">Ресурсы URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="cba94-102">Resources URI for Excel Services REST API</span></span>

<span data-ttu-id="cba94-103">Непосредственно с помощью API-Интерфейс REST в Службы Excel можно связать сущности.</span><span class="sxs-lookup"><span data-stu-id="cba94-103">You can link to entities directly by using the REST API in Excel Services.</span></span>
  
> [!NOTE]
> <span data-ttu-id="cba94-104">API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="cba94-104">The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="cba94-105">Для учетных записей Office 365 для образования, Office 365 бизнес и Office 365 корпоративный используйте REST API Excel, входящие в состав конечной точки [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
).</span><span class="sxs-lookup"><span data-stu-id="cba94-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="base-rest-url"></a><span data-ttu-id="cba94-106">URL-адрес базовый REST</span><span class="sxs-lookup"><span data-stu-id="cba94-106">Base REST URL</span></span>

<span data-ttu-id="cba94-107">Ниже приведен пример URL-адреса REST конкретного элемента в книге.</span><span class="sxs-lookup"><span data-stu-id="cba94-107">The following is an example of a REST URL to a specific element in a workbook.</span></span>
  
    
    

```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

<span data-ttu-id="cba94-p102">Относительный URL-адрес REST зависит от базовый URL-адрес REST. Ниже приведен пример базовый URL-адрес REST для конкретной книги.</span><span class="sxs-lookup"><span data-stu-id="cba94-p102">A relative REST URL is based off the base REST URL. The following is an example of a base REST URL to a specific workbook.</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>
```

<span data-ttu-id="cba94-110">Например, если у вас есть книгу с именем «sampleWorkbook.xlsx» в библиотеке документов, следующие:</span><span class="sxs-lookup"><span data-stu-id="cba94-110">For example, if you have a workbook named "sampleWorkbook.xlsx" in the following document library:</span></span> 
  
    
    



```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

<span data-ttu-id="cba94-111"> Это базовый URL-адрес REST в книге:</span><span class="sxs-lookup"><span data-stu-id="cba94-111">The base REST URL to the workbook is:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx
```


## <a name="resources-uri"></a><span data-ttu-id="cba94-112">URI-код ресурсов</span><span class="sxs-lookup"><span data-stu-id="cba94-112">Resources URI</span></span>

<span data-ttu-id="cba94-p103">В таблице 1 приведены всех доступных ресурсах в Службы Excel API-интерфейса REST. Для доступа к определенному ресурсу, добавьте расположение ресурсов базовый URL-адрес REST в книгу.</span><span class="sxs-lookup"><span data-stu-id="cba94-p103">Table 1 shows all the accessible resources in the Excel Services REST API. To access a particular resource, append the resource location to the base REST URL to a workbook.</span></span>
  
    
    

<span data-ttu-id="cba94-115">**В таблице 1. Ресурсы, доступных в API REST служб Excel**</span><span class="sxs-lookup"><span data-stu-id="cba94-115">**Table 1. Accessible resources in the Excel Services REST API**</span></span>


|<span data-ttu-id="cba94-116">**Расположение ресурсов**</span><span class="sxs-lookup"><span data-stu-id="cba94-116">**Resource Location**</span></span>|<span data-ttu-id="cba94-117">**Формат**</span><span class="sxs-lookup"><span data-stu-id="cba94-117">**Format**</span></span>|<span data-ttu-id="cba94-118">**Пример**</span><span class="sxs-lookup"><span data-stu-id="cba94-118">**Example**</span></span>|<span data-ttu-id="cba94-119">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="cba94-119">**Notes**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="cba94-120">/ модель</span><span class="sxs-lookup"><span data-stu-id="cba94-120">/model</span></span>  <br/> |<span data-ttu-id="cba94-121">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-121">Atom (default)</span></span>  <br/> |<span data-ttu-id="cba94-122">/ модель</span><span class="sxs-lookup"><span data-stu-id="cba94-122">/model</span></span>  <br/> |<span data-ttu-id="cba94-p104">Возвращает канала с ресурсами, поддерживаемый Службы Excel API-Интерфейс REST Atom. Поддерживаемые ресурсы, диапазоны, диаграмм, таблиц и сводных таблиц.</span><span class="sxs-lookup"><span data-stu-id="cba94-p104">Returns an Atom feed with the resources supported by the Excel Services REST API. The supported resources are ranges, charts, tables, and PivotTables.</span></span>  <br/> |
|<span data-ttu-id="cba94-125">аудио- и модель</span><span class="sxs-lookup"><span data-stu-id="cba94-125">/model</span></span>  <br/> |<span data-ttu-id="cba94-126">workbook</span><span class="sxs-lookup"><span data-stu-id="cba94-126">workbook</span></span>  <br/> |<span data-ttu-id="cba94-127">аудио- и модель? $format = книги</span><span class="sxs-lookup"><span data-stu-id="cba94-127">/model?$format=workbook</span></span>  <br/> |<span data-ttu-id="cba94-p105">Это рабочей книги. Поддерживаемые книги форматов, xlsx, xlsb и xlsm.</span><span class="sxs-lookup"><span data-stu-id="cba94-p105">This is the workbook. Supported workbook formats are xlsx, xlsb, and xlsm.</span></span>  <br/> |
|<span data-ttu-id="cba94-130">/ модели/диапазонов</span><span class="sxs-lookup"><span data-stu-id="cba94-130">/model/Ranges</span></span>  <br/> |<span data-ttu-id="cba94-131">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-131">Atom (default)</span></span>  <br/> |<span data-ttu-id="cba94-132">Диапазоны/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="cba94-132">/model/Ranges?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-133">Веб-канала Atom, listis всех именованных диапазонов в книге.</span><span class="sxs-lookup"><span data-stu-id="cba94-133">An Atom feed that listis all the named ranges in the workbook.</span></span>  <br/> |
|<span data-ttu-id="cba94-134">/Model/Ranges('[name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-134">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-135">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-135">HTML (default)</span></span>  <br/> |<span data-ttu-id="cba94-136">/model/Ranges('MyRange')?$format=html</span><span class="sxs-lookup"><span data-stu-id="cba94-136">/model/Ranges('MyRange')?$format=html</span></span>  <br/> |<span data-ttu-id="cba94-137">Фрагмент HTML-кода для запрошенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="cba94-137">An HTML fragment for the requested range.</span></span>  <br/> |
|<span data-ttu-id="cba94-138">/Model/Ranges('[name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-138">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-139">Atom</span><span class="sxs-lookup"><span data-stu-id="cba94-139">Atom</span></span>  <br/> |<span data-ttu-id="cba94-140">/model/Ranges('MyRange')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="cba94-140">/model/Ranges('MyRange')?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-141">Запись Atom, содержащий XML-представление данных в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="cba94-141">An Atom entry that contains an XML representation of the data within the range.</span></span>  <br/> |
|<span data-ttu-id="cba94-142">/ модели/диаграмм</span><span class="sxs-lookup"><span data-stu-id="cba94-142">/model/Charts</span></span>  <br/> |<span data-ttu-id="cba94-143">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-143">Atom (default)</span></span>  <br/> |<span data-ttu-id="cba94-144">Диаграммы/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="cba94-144">/model/Charts?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-145">Канала Atom, в котором приведены все диаграммы в книге.</span><span class="sxs-lookup"><span data-stu-id="cba94-145">An Atom feed that lists all the charts in the workbook.</span></span>  <br/> |
|<span data-ttu-id="cba94-146">/Model/Charts('[name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-146">/model/Charts('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-147">Изображение (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-147">Image (default)</span></span>  <br/> |<span data-ttu-id="cba94-148">/model/Charts('MyChart')?$format=image</span><span class="sxs-lookup"><span data-stu-id="cba94-148">/model/Charts('MyChart')?$format=image</span></span>  <br/> |<span data-ttu-id="cba94-p106">Изображение диаграммы.  Это изображение в формате Portable Network Graphics (PNG).</span><span class="sxs-lookup"><span data-stu-id="cba94-p106">An image of the chart. The image is in Portable Network Graphics (PNG) format.</span></span>  <br/> |
|<span data-ttu-id="cba94-151">/ модели/таблиц</span><span class="sxs-lookup"><span data-stu-id="cba94-151">/model/Tables</span></span>  <br/> |<span data-ttu-id="cba94-152">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-152">Atom (default)</span></span>  <br/> |<span data-ttu-id="cba94-153">Таблицы/модели /? $format = atom</span><span class="sxs-lookup"><span data-stu-id="cba94-153">/model/Tables?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-154">Канала Atom, который перечисляет все таблицы, доступные в книге.</span><span class="sxs-lookup"><span data-stu-id="cba94-154">An Atom feed that lists all the available tables in the workbook.</span></span>  <br/> |
|<span data-ttu-id="cba94-155">/Model/Tables('[name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-155">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-156">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-156">HTML (default)</span></span>  <br/> |<span data-ttu-id="cba94-157">/model/Tables('MyTable')?$format=html</span><span class="sxs-lookup"><span data-stu-id="cba94-157">/model/Tables('MyTable')?$format=html</span></span>  <br/> |<span data-ttu-id="cba94-158">Фрагмент HTML-кода для запрошенного таблицы.</span><span class="sxs-lookup"><span data-stu-id="cba94-158">An HTML fragment for the requested table.</span></span>  <br/> |
|<span data-ttu-id="cba94-159">/Model/Tables('[name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-159">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-160">Atom</span><span class="sxs-lookup"><span data-stu-id="cba94-160">Atom</span></span>  <br/> |<span data-ttu-id="cba94-161">/model/Tables('MyTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="cba94-161">/model/Tables('MyTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-162">Запись Atom, содержащий XML-представление данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="cba94-162">An Atom entry that contains an XML representation of the data within the table.</span></span>  <br/> |
|<span data-ttu-id="cba94-163">/model/PivotTables</span><span class="sxs-lookup"><span data-stu-id="cba94-163">/model/PivotTables</span></span>  <br/> |<span data-ttu-id="cba94-164">Atom (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-164">Atom (default)</span></span>  <br/> |<span data-ttu-id="cba94-165">/model/PivotTables?$format=atom</span><span class="sxs-lookup"><span data-stu-id="cba94-165">/model/PivotTables?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-166">Канала Atom, в котором приведены все доступные сводных таблиц в книге</span><span class="sxs-lookup"><span data-stu-id="cba94-166">An Atom feed that lists all the available PivotTables in the workbook</span></span>  <br/> |
|<span data-ttu-id="cba94-167">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-167">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-168">HTML (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cba94-168">HTML (default)</span></span>  <br/> |<span data-ttu-id="cba94-169">/model/PivotTables('MyPivotTable)?$format=html</span><span class="sxs-lookup"><span data-stu-id="cba94-169">/model/PivotTables('MyPivotTable)?$format=html</span></span>  <br/> |<span data-ttu-id="cba94-170">Фрагмент HTML-кода для запрошенного сводных таблиц.</span><span class="sxs-lookup"><span data-stu-id="cba94-170">An HTML fragment for the requested PivotTable.</span></span>  <br/> |
|<span data-ttu-id="cba94-171">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="cba94-171">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="cba94-172">Atom</span><span class="sxs-lookup"><span data-stu-id="cba94-172">Atom</span></span>  <br/> |<span data-ttu-id="cba94-173">/model/PivotTables('MyPivotTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="cba94-173">/model/PivotTables('MyPivotTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="cba94-174">Запись Atom, содержащий XML-представление данных в сводных таблицах.</span><span class="sxs-lookup"><span data-stu-id="cba94-174">An Atom entry that contains an XML representation of the data within the PivotTables.</span></span>  <br/> |
   
> [!NOTE]
> <span data-ttu-id="cba94-p107">[!Примечание] Службы Excel ограничивает количество диапазоны, которые можно включить в URL-адрес для 10. При наличии более 10 диапазонов в URL-адрес, вы получите сообщение о том, что служба недоступна.</span><span class="sxs-lookup"><span data-stu-id="cba94-p107">Excel Services limits the number of ranges that you can include in a URL to 10. If you include more than 10 Ranges in a URL, you will get an error that indicates that the service is unavailable.</span></span> 

## <a name="see-also"></a><span data-ttu-id="cba94-177">См. также</span><span class="sxs-lookup"><span data-stu-id="cba94-177">See also</span></span>

- [<span data-ttu-id="cba94-178">Структура базового URI и путь</span><span class="sxs-lookup"><span data-stu-id="cba94-178">Basic URI Structure and Path</span></span>](basic-uri-structure-and-path.md)
