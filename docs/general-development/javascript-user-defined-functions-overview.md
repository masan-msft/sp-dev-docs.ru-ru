---
title: "Общие сведения о пользовательских функций JavaScript"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fee38837-1985-4319-ba4e-b99c6ec66336
ms.openlocfilehash: f154b2ba19fd37bb51ec4ada82ed5e6ce47b3006
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="javascript-user-defined-functions-overview"></a>Общие сведения о пользовательских функций JavaScript
JavaScript пользовательские функции (UDF) являются новыми в службах Excel в SharePoint. В этой статье предоставляет подробный обзор пользовательских функций JavaScript, в том числе основные сведения о работе в службах Excel.
## <a name="what-are-udfs"></a>Что такое пользовательских функций
<a name="xlsWhatAreUdfs"> </a>

Пользовательские функции (UDF)  это функция самостоятельно создать и затем добавить в список доступных функций в Excel при Excel не предоставляет тип функции, которые должны сразу же после установки.
  
    
    
Службы Excel уже позволяет создавать пользовательские функции с помощью управляемого кода, поэтому если вы работали с существующим Службы Excel пользовательских функций, пользовательских функций JavaScript должны быть знакомы вам. Дополнительные сведения о создании пользовательских функций с помощью управляемого кода можно  [Excel Services User-Defined Functions](excel-services-user-defined-functions.md).
  
    
    

## <a name="javascript-udfs"></a>Пользовательские функции JavaScript
<a name="xlsJsUDFs"> </a>

Пользовательские функции JavaScript, пользовательских функций, которые запускаются в браузере на веб-страницу, состоит в книге внедренных Excel. Используйте JavaScript UDF внутри внедренной книги. До тех пор, пока вы работаете с книгой в браузере, можно использовать JavaScript UDF так же, как использовать функции встроенных Excel. При закрытии веб-страницы в JavaScript UDF больше не доступен.
  
    
    

## <a name="how-do-javascript-udfs-work"></a>Как работают JavaScript UDF?
<a name="xlsJsUDFs"> </a>

Чтобы использовать JavaScript UDF, необходимо иметь возможность изменения содержимого веб-страницы, где внедрить эту книгу. После добавления ссылки к исходному файлу правильные Службы Excel JavaScript, добавьте код JavaScript UDF на страницу. Кроме того прежде чем использовать JavaScript UDF, сначала необходимо зарегистрировать пользовательскую Функцию в Службы вычислений Excel. JavaScript UDF API предоставляет методы для регистрации и отмены регистрации JavaScript UDF.
  
    
    
Когда веб-страница с Excel веб-части Web Access или внедренной книги, можно вызвать JavaScript UDF в книге, как и любой другой Excel книги.
  
    
    
Например имеется функция, которая получает текущий акций для указанного актива. Можно добавить JavaScript UDF на веб-страницу, на котором размещается книги Excel (предполагается, что у вас есть авторские права для веб-страницы), которые использует JavaScript код следующим образом.
  
    
    



```

function StockInfo(symbol, measure) {
  var req = new XMLHttpRequest();
  req.open('GET', 'http://www.contoso-stock-quotes.com/quote/' + symbol + '/' + measure, false); 
  req.send(null);
  if (req.status == 200) {
    return req.responseText;
  } else {
    throw new Error(ExcelCalcError.Value);
  }
 
ewa.BrowserUdfs.add("StockQuote",
                       StockInfo,
                       "Gets a stock quote given a security symbol and measure to return."
                       false,
                       false
                       );

```

Затем можно назвать JavaScript UDF, StockInfo, в формуле из ячейки внутри Excel Online.
  
    
    

**На рисунке 1. Вызов JavaScript UDF в Excel Online**

  
    
    

  
    
    
![Вызов JavaScript UDF в Excel Online](../images/SPS15CON_xls_JsUdfinWebApp.jpg)
  
    
    

  
    
    

  
    
    

## <a name="where-can-i-use-javascript-udfs"></a>Где можно использовать пользовательские функции JavaScript?
<a name="xlsWhereUseJsUdfs"> </a>

Можно создавать и использовать пользовательские функции JavaScript на книгах, отображаемые в веб-частей SharePoint Excel Web Access или на веб-страницу узла с внедренной книгой. Книги должны быть сохранены на Microsoft OneDrive. Основное различие заключается в том, что пользовательские функции JavaScript, добавить веб-части Excel Web Access требуется SharePoint server. Пользовательские функции JavaScript, добавлена для размещения веб-страницы, внедренной книги требуется только сохранение книги на OneDrive.
  
    
    

## <a name="key-points"></a>Ключевые моменты
<a name="xlsWhereUseJsUdfs"> </a>


- Пользовательские функции JavaScript только live до тех пор, пока они находятся на веб-страницей, отображается. Они не сохраняются после истечения времени жизни веб-страницы, где они были созданы.
    
  
- Нельзя выполнять вызовы Службы Excel объектной модели JavaScript из в JavaScript UDF.
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Службы Excel в SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Новые возможности служб Excel для разработчиков](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [Пользовательские функции служб Excel](http://msdn.microsoft.com/en-us/library/ms493934)
    
  

