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
# <a name="resources-uri-for-excel-services-rest-api"></a>Ресурсы URI для интерфейса API REST служб Excel

Непосредственно с помощью API-Интерфейс REST в Службы Excel можно связать сущности.
  
    
    


> **Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.
  
    
    


## <a name="base-rest-url"></a>URL-адрес базовый REST

Ниже приведен пример URL-адреса REST конкретного элемента в книге.
  
    
    

```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

Относительный URL-адрес REST зависит от базовый URL-адрес REST. Ниже приведен пример базовый URL-адрес REST для конкретной книги.
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>
```

Например, если у вас есть книгу с именем «sampleWorkbook.xlsx» в библиотеке документов, следующие: 
  
    
    



```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

 Это базовый URL-адрес REST в книге:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx
```


## <a name="resources-uri"></a>URI-код ресурсов

В таблице 1 приведены всех доступных ресурсах в Службы Excel API-интерфейса REST. Для доступа к определенному ресурсу, добавьте расположение ресурсов базовый URL-адрес REST в книгу.
  
    
    

**В таблице 1. Ресурсы, доступных в API REST служб Excel**


|**Расположение ресурсов**|**Формат**|**Пример**|**Примечания**|
|:-----|:-----|:-----|:-----|
|/ модель  <br/> |Atom (по умолчанию)  <br/> |/ модель  <br/> |Возвращает канала с ресурсами, поддерживаемый Службы Excel API-Интерфейс REST Atom. Поддерживаемые ресурсы, диапазоны, диаграмм, таблиц и сводных таблиц.  <br/> |
|аудио- и модель  <br/> |workbook  <br/> |аудио- и модель? $format = книги  <br/> |Это рабочей книги. Поддерживаемые книги форматов, xlsx, xlsb и xlsm.  <br/> |
|/ модели/диапазонов  <br/> |Atom (по умолчанию)  <br/> |Диапазоны/модели /? $format = atom  <br/> |Веб-канала Atom, listis всех именованных диапазонов в книге.  <br/> |
|/Model/Ranges('[name]')  <br/> |HTML (по умолчанию)  <br/> |/model/Ranges('MyRange')?$format=html  <br/> |Фрагмент HTML-кода для запрошенного диапазона.  <br/> |
|/Model/Ranges('[name]')  <br/> |Atom  <br/> |/model/Ranges('MyRange')?$format=atom  <br/> |Запись Atom, содержащий XML-представление данных в диапазоне.  <br/> |
|/ модели/диаграмм  <br/> |Atom (по умолчанию)  <br/> |Диаграммы/модели /? $format = atom  <br/> |Канала Atom, в котором приведены все диаграммы в книге.  <br/> |
|/Model/Charts('[name]')  <br/> |Изображение (по умолчанию)  <br/> |/model/Charts('MyChart')?$format=image  <br/> |Изображение диаграммы.  Это изображение в формате Portable Network Graphics (PNG).  <br/> |
|/ модели/таблиц  <br/> |Atom (по умолчанию)  <br/> |Таблицы/модели /? $format = atom  <br/> |Канала Atom, который перечисляет все таблицы, доступные в книге.  <br/> |
|/Model/Tables('[name]')  <br/> |HTML (по умолчанию)  <br/> |/model/Tables('MyTable')?$format=html  <br/> |Фрагмент HTML-кода для запрошенного таблицы.  <br/> |
|/Model/Tables('[name]')  <br/> |Atom  <br/> |/model/Tables('MyTable')?$format=atom  <br/> |Запись Atom, содержащий XML-представление данных в таблице.  <br/> |
|/model/PivotTables  <br/> |Atom (по умолчанию)  <br/> |/model/PivotTables?$format=atom  <br/> |Канала Atom, в котором приведены все доступные сводных таблиц в книге  <br/> |
|/model/PivotTables('[Name]')  <br/> |HTML (по умолчанию)  <br/> |/model/PivotTables('MyPivotTable)?$format=html  <br/> |Фрагмент HTML-кода для запрошенного сводных таблиц.  <br/> |
|/model/PivotTables('[Name]')  <br/> |Atom  <br/> |/model/PivotTables('MyPivotTable')?$format=atom  <br/> |Запись Atom, содержащий XML-представление данных в сводных таблицах.  <br/> |
   

> **Примечание:** Службы Excel — ограничивает число диапазоны, которые можно включить в URL-адреса до 10. Если включить более 10 диапазоны в URL-адрес, вы получите сообщение о том, что служба недоступна. 
  
    
    


## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Основные понятия


  
    
    
 [Структура базового URI и путь](basic-uri-structure-and-path.md)
