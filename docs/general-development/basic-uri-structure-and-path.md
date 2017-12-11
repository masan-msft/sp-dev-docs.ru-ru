---
title: "Структура базового URI и путь"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d73cf6c2-0677-4726-8a3e-2ad130e1a12c
ms.openlocfilehash: 3cb8133b01c2a7ec88e954c6a455e80677b53b38
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="basic-uri-structure-and-path"></a>Структура базового URI и путь

В этом разделе объясняется, как создать URI структуры и путь для команды службы REST в Службы Excel.
  
> [!NOTE]
> 
> API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для учетных записей Office 365 для образования, Office 365 бизнес и Office 365 корпоративный используйте REST API Excel, входящие в состав конечной точки [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
).
  
    
    


## <a name="basic-url-structure-and-path"></a>Структура базового URL-адреса и пути

API-Интерфейс REST в Службы Excel дает возможность получить доступ к ресурсам как диаграммы, сводные таблицы, таблиц и именованных диапазонов в книге непосредственно через URL-адрес. Каждый URL-адрес REST в Службы Excel построения из трех частей. Ниже представлена базовая структура URL-адреса для доступа к ресурсам в книге: 
  
    
    

1. **REST aspx URI страницы** Точка входа в страницу ASPX
    
  
2. **Расположение книги** Путь к книге
    
  
3. **Расположение ресурсов** Путь к запрошенному ресурсу внутри книги
    
  
Ниже приведен пример URL-адреса REST конкретного элемента в книге:
  
    
    



```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

Ниже приведен пример вид URL-адреса REST в Службы Excel все три части в сочетании. В этом примере URL-адреса REST обращается к книги с названием «sampleWorkbook.xlsx», который содержит диаграммы, называется «SampleChart»:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart')
```

Книга хранится в библиотеке документов. Полный путь к книге  _<ServerName>_ `http://` `/Docs/Documents/sampleWorkbook.xlsx`.
  
    
    
Три части URL-адрес REST следующие:
  
    
    

1. **REST aspx URI страницы**: _<ServerName>_ `http://` `/_vti_bin/ExcelRest.aspx`
    
  
2. **Расположение книги**: `/Docs/Documents/sampleWorkbook.xlsx`
    
  
3. **Расположение ресурса**: `/model/Ranges('nameOfTheNamedRange')`
    
  

### <a name="accessing-by-using-the-discovery-user-interface"></a>Доступ к с помощью пользовательского интерфейса обнаружения

Можно также получить доступ к диаграмме с помощью пользовательского интерфейса обнаружения. Чтобы получить доступ к ресурсам как диаграммы, таблицы, сводные таблицы и диапазонов с помощью механизма обнаружения, показано на следующем снимке экрана, обратитесь к разделу  [Обнаружение в API REST служб Excel](discovery-in-excel-services-rest-api.md).
  
    
    

  
    
    
![URL-адрес модели REST служб Excel](../images/SharePointServer14Con_XLSvcs_RESTModel.gif)
  
    
    

  
    
    

  
    
    

  
    
    

### <a name="marker-path"></a>Путь в маркер

Ниже приведен на aspx-странице для службы REST в Службы Excel:
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```

Для доступа к службе REST в Службы Excel, необходимо перед ввести URL-адрес с _<ServerName>_ `http://` `/_vti_bin/ExcelRest.aspx`.
  
    
    

### <a name="workbook-location"></a>Расположение книги

Расположение книги  это относительный путь к книге, которая содержит ресурсы, которые нуждаются в доступе к. Например предположим, что у вас есть книгу с именем sampleWorkbook.xlsx, сохраненный на надежной библиотеки документов SharePoint. В этом примере следующие  это путь к папке sampleWorkbook.xlsx: 
  
    
    

```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

Выполните относительный путь к книге ( `Docs/Documents/sampleWorkbook.xlsx`) и добавьте к пути маркер. Ниже приведен URL-адрес с добавленным расположением книгу и путь маркер.
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```


### <a name="resource-location"></a>Расположение ресурсов

Расположение ресурсов  это путь внутри книги в элемент при запросе. Например если вы хотите получить диаграммы, расположение ресурсов будет выглядеть  `/model/Charts('Chart 1')`.
  
    
    
Полный URL-адрес добавьте это маркер путь и относительный путь к книге. Ниже приведен полный пример URL-адреса:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```


## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Основные понятия


  
    
    
 [Ресурсы URI для интерфейса API REST служб Excel](resources-uri-for-excel-services-rest-api.md)
  
    
    
 [Обнаружение в API REST служб Excel](discovery-in-excel-services-rest-api.md)
