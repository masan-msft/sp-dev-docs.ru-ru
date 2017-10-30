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
# <a name="sample-uri-for-excel-services-rest-api"></a>Пример URI для интерфейса API REST служб Excel

В этом разделе приведены примеры коды URI для команды службы передачи (REST) представлений состояний в Службы Excel.
  
    
    


> **Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.
  
    
    


## <a name="sample-uri-for-rest-commands-in-excel-services"></a>Пример URI для команды REST в службах Excel

В следующих примерах каждый из URI ссылается на книгу с именем  *sampleWorkbook.xlsx*  .
  
    
    

- Файл sampleWorkbook.xlsx содержит именованные диапазоны и диаграммы.
    
  
- Файл sampleWorkbook.xlsx сохраняется в надежной библиотеке документов SharePoint. В этом примере  это путь к папке sampleWorkbook.xlsx:
    
```
  
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```


### <a name="sample-uri"></a>Пример URI

На странице ASPX для службы REST в Службы Excel  это: 
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx

```

Ниже приведены коды URI для получения доступа к книгам sampleWorkbook.xlsx с помощью службы REST в Службы Excel примере. 
  
    
    

- Модель верхнего уровня для книги (только диапазонов и диаграмм в текущем построении):
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model

```

- Получение полного книги:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=workbook

```

- Возвращает диапазон (по умолчанию html). Следующие два примера URI эквивалентны:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')

```


```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?$format=html
```

- Получение именованный диапазон:
    
```
  http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('nameOfTheNamedRange')

```

- Возвращать канал Atom XML:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=atom

```

- Задайте ячейки и вернуть его.
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?Ranges('Sheet1!C3')=demo

```

- Получение диаграммы:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```

- Задайте значение и получить диаграммы:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?Ranges('Sheet1!A1')=5.5

```


