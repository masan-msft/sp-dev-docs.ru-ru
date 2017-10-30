---
title: "Доступ к схеме"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 02613912-36f6-4edc-a915-165d12e60bc8
ms.openlocfilehash: 9f9bb2513eb8c2dbbe5951d86391ebb239a6c389
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-a-schema"></a>Доступ к схеме

В этом разделе показано один пример того, как можно получить доступ к и просмотрите схемы для службы REST в Службы Excel. В этом разделе предполагается, что вы прочли  [Пример URI для интерфейса API REST служб Excel](sample-uri-for-excel-services-rest-api.md).d
  
    
    


> **Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для образовательных учреждений Office 365, бизнеса и корпоративных учетных записей используйте Excel API-интерфейсы REST, входящих в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> ) конечной точки.
  
    
    


## <a name="viewing-a-schema"></a>Просмотр схемы

 В адресной строке браузера введите URI для Atom XML веб-канал с помощью URI, как показано ниже:
  
    
    

```

http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|H3')?$format=atom
```

Щелкните правой кнопкой мыши веб-страницы и нажмите кнопку **Просмотреть исходный код**.
  
    
    
Вы должны увидеть схему, которая выглядит примерно следующим образом:
  
    
    



```XML
<?xml version="1.0" encoding="utf-8"?>
<entry xml:base="http://excel.live.com/REST" xmlns:x="http://schemas.microsoft.com/office/2008/07/excelservices/rest" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservice" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
  <title type="text">Sheet1!A1:H3</title>
  <id>http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1%7CH3')</id>
  <updated>2009-06-25T00:41:37Z</updated>
  <author>
    <name />
  </author>
  <link rel="self" href="http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1%7CH3')?$format=atom" title="Sheet1!A1:H3" />
  <category term="ExcelServices.Range" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <content type="application/xml">
    <x:range name="Sheet1!A1:H3">
      <x:row>
        <x:c>
          <x:fv>Name </x:fv>
        </x:c>
        <x:c>
          <x:fv>Name </x:fv>
        </x:c>
        <x:c>
          <x:fv>Exchange  </x:fv>
        </x:c>
        <x:c>
          <x:fv>Symbol  </x:fv>
        </x:c>
        <x:c>
          <x:fv>Last Trade </x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>Change </x:fv>
        </x:c>
        <x:c>
          <x:fv>Mkt Cap</x:fv>
        </x:c>
      </x:row>
      <x:row>
        <x:c>
          <x:fv>Microsoft Corporation </x:fv>
        </x:c>
        <x:c>
          <x:fv>Microsoft Corporation </x:fv>
        </x:c>
        <x:c>
          <x:fv> </x:fv>
        </x:c>
        <x:c>
          <x:fv>MSFT </x:fv>
        </x:c>
        <x:c>
          <x:v>26.25</x:v>
          <x:fv>26.25</x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>-0.23 (-0.87%) </x:fv>
        </x:c>
        <x:c>
          <x:v>239670000000</x:v>
          <x:fv> $239,670,000,000 </x:fv>
        </x:c>
      </x:row>
      <x:row>
        <x:c />
        <x:c />
        <x:c>
          <x:fv> </x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:v>15.58</x:v>
          <x:fv>15.58</x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>-1.38 (-8.14%) </x:fv>
        </x:c>
        <x:c>
          <x:v>21590000000</x:v>
          <x:fv> $21,590,000,000 </x:fv>
        </x:c>
      </x:row>
    </x:range>
  </content>
</entry>

```


