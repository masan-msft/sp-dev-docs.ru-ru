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
# <a name="javascript-user-defined-functions-overview"></a><span data-ttu-id="d1fe7-102">Общие сведения о пользовательских функций JavaScript</span><span class="sxs-lookup"><span data-stu-id="d1fe7-102">JavaScript user-defined functions overview</span></span>
<span data-ttu-id="d1fe7-103">JavaScript пользовательские функции (UDF) являются новыми в службах Excel в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-103">JavaScript user-defined functions (UDFs) are new in Excel Services in SharePoint.</span></span> <span data-ttu-id="d1fe7-104">В этой статье предоставляет подробный обзор пользовательских функций JavaScript, в том числе основные сведения о работе в службах Excel.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-104">This article provides a high-level look at JavaScript UDFs, including basic information on how they work in Excel Services.</span></span>
## <a name="what-are-udfs"></a><span data-ttu-id="d1fe7-105">Что такое пользовательских функций</span><span class="sxs-lookup"><span data-stu-id="d1fe7-105">What are UDFs?</span></span>
<span data-ttu-id="d1fe7-106"><a name="xlsWhatAreUdfs"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-106"><a name="xlsWhatAreUdfs"> </a></span></span>

<span data-ttu-id="d1fe7-107">Пользовательские функции (UDF)  это функция самостоятельно создать и затем добавить в список доступных функций в Excel при Excel не предоставляет тип функции, которые должны сразу же после установки.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-107">A user-defined function (UDF) is a function that you can create yourself and then add to the list of available functions in Excel when Excel doesn't provide the type of function that you want right out of the box.</span></span>
  
    
    
<span data-ttu-id="d1fe7-p102">Службы Excel уже позволяет создавать пользовательские функции с помощью управляемого кода, поэтому если вы работали с существующим Службы Excel пользовательских функций, пользовательских функций JavaScript должны быть знакомы вам. Дополнительные сведения о создании пользовательских функций с помощью управляемого кода можно  [Excel Services User-Defined Functions](excel-services-user-defined-functions.md).</span><span class="sxs-lookup"><span data-stu-id="d1fe7-p102">Excel Services already allows you to create UDFs using managed code, so if you have worked with the existing Excel Services UDFs, JavaScript UDFs should look familiar to you. For more information about creating UDFs using managed code, see  [Excel Services User-Defined Functions](excel-services-user-defined-functions.md).</span></span>
  
    
    

## <a name="javascript-udfs"></a><span data-ttu-id="d1fe7-110">Пользовательские функции JavaScript</span><span class="sxs-lookup"><span data-stu-id="d1fe7-110">JavaScript UDFs</span></span>
<span data-ttu-id="d1fe7-111"><a name="xlsJsUDFs"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-111"><a name="xlsJsUDFs"> </a></span></span>

<span data-ttu-id="d1fe7-p103">Пользовательские функции JavaScript, пользовательских функций, которые запускаются в браузере на веб-страницу, состоит в книге внедренных Excel. Используйте JavaScript UDF внутри внедренной книги. До тех пор, пока вы работаете с книгой в браузере, можно использовать JavaScript UDF так же, как использовать функции встроенных Excel. При закрытии веб-страницы в JavaScript UDF больше не доступен.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-p103">JavaScript UDFs are UDFs that run in the browser on a webpage that has an embedded Excel workbook. You use the JavaScript UDF inside of the embedded workbook. As long as you are working with the workbook in the browser, you can use the JavaScript UDF just like you use the built-in Excel functions. When the webpage is closed, the JavaScript UDF is no longer available.</span></span>
  
    
    

## <a name="how-do-javascript-udfs-work"></a><span data-ttu-id="d1fe7-116">Как работают JavaScript UDF?</span><span class="sxs-lookup"><span data-stu-id="d1fe7-116">How do JavaScript UDFs work?</span></span>
<span data-ttu-id="d1fe7-117"><a name="xlsJsUDFs"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-117"><a name="xlsJsUDFs"> </a></span></span>

<span data-ttu-id="d1fe7-p104">Чтобы использовать JavaScript UDF, необходимо иметь возможность изменения содержимого веб-страницы, где внедрить эту книгу. После добавления ссылки к исходному файлу правильные Службы Excel JavaScript, добавьте код JavaScript UDF на страницу. Кроме того прежде чем использовать JavaScript UDF, сначала необходимо зарегистрировать пользовательскую Функцию в Службы вычислений Excel. JavaScript UDF API предоставляет методы для регистрации и отмены регистрации JavaScript UDF.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-p104">To use a JavaScript UDF, you have to have the ability to modify the content of the webpage where you embed the workbook. After you reference the correct Excel Services JavaScript source file, you add your JavaScript UDF code to the page. Additionally, before you use your JavaScript UDF, you first have to register the UDF with the Excel Calculation Services. The JavaScript UDF API provides methods to both register and unregister your JavaScript UDF.</span></span>
  
    
    
<span data-ttu-id="d1fe7-122">Когда веб-страница с Excel веб-части Web Access или внедренной книги, можно вызвать JavaScript UDF в книге, как и любой другой Excel книги.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-122">When the webpage with the Excel Web Access Web Part or embedded workbook renders, you can invoke the JavaScript UDF in the workbook just like any other Excel workbook.</span></span>
  
    
    
<span data-ttu-id="d1fe7-p105">Например имеется функция, которая получает текущий акций для указанного актива. Можно добавить JavaScript UDF на веб-страницу, на котором размещается книги Excel (предполагается, что у вас есть авторские права для веб-страницы), которые использует JavaScript код следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-p105">For example, you may have a function that gets the current stock price for a specific stock. You could add a JavaScript UDF to the webpage that hosts your Excel workbook (assuming you have authoring rights for the webpage) that uses JavaScript code as follows.</span></span>
  
    
    



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

<span data-ttu-id="d1fe7-125">Затем можно назвать JavaScript UDF, StockInfo, в формуле из ячейки внутри Excel Online.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-125">You could then call the JavaScript UDF, StockInfo, in a formula from a cell inside the Excel Online.</span></span>
  
    
    

<span data-ttu-id="d1fe7-126">**На рисунке 1. Вызов JavaScript UDF в Excel Online**</span><span class="sxs-lookup"><span data-stu-id="d1fe7-126">**Figure 1. JavaScript UDF invoked in Excel Online**</span></span>

  
    
    

  
    
    
![Вызов JavaScript UDF в Excel Online](../images/SPS15CON_xls_JsUdfinWebApp.jpg)
  
    
    

  
    
    

  
    
    

## <a name="where-can-i-use-javascript-udfs"></a><span data-ttu-id="d1fe7-128">Где можно использовать пользовательские функции JavaScript?</span><span class="sxs-lookup"><span data-stu-id="d1fe7-128">Where can I use JavaScript UDFs?</span></span>
<span data-ttu-id="d1fe7-129"><a name="xlsWhereUseJsUdfs"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-129"><a name="xlsWhereUseJsUdfs"> </a></span></span>

<span data-ttu-id="d1fe7-130">Можно создавать и использовать пользовательские функции JavaScript на книгах, отображаемые в веб-частей SharePoint Excel Web Access или на веб-страницу узла с внедренной книгой.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-130">You can create and use JavaScript UDFs either on workbooks displayed in SharePoint Excel Web Access Web Parts or on a host webpage that has an embedded workbook.</span></span> <span data-ttu-id="d1fe7-131">Книги должны быть сохранены на Microsoft OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-131">The workbook must be stored on Microsoft OneDrive.</span></span> <span data-ttu-id="d1fe7-132">Основное различие заключается в том, что пользовательские функции JavaScript, добавить веб-части Excel Web Access требуется SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-132">The main difference is that JavaScript UDFs added to Excel Web Access Web Parts require a SharePoint server.</span></span> <span data-ttu-id="d1fe7-133">Пользовательские функции JavaScript, добавлена для размещения веб-страницы, внедренной книги требуется только сохранение книги на OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-133">JavaScript UDFs added to host webpages that have embedded workbooks require only that the workbook be stored on OneDrive.</span></span>
  
    
    

## <a name="key-points"></a><span data-ttu-id="d1fe7-134">Ключевые моменты</span><span class="sxs-lookup"><span data-stu-id="d1fe7-134">Key points</span></span>
<span data-ttu-id="d1fe7-135"><a name="xlsWhereUseJsUdfs"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-135"><a name="xlsWhereUseJsUdfs"> </a></span></span>


- <span data-ttu-id="d1fe7-p107">Пользовательские функции JavaScript только live до тех пор, пока они находятся на веб-страницей, отображается. Они не сохраняются после истечения времени жизни веб-страницы, где они были созданы.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-p107">JavaScript UDFs only live as long as the webpage they are on is being displayed. They do not persist beyond the lifetime of the webpage where they were created.</span></span>
    
  
- <span data-ttu-id="d1fe7-138">Нельзя выполнять вызовы Службы Excel объектной модели JavaScript из в JavaScript UDF.</span><span class="sxs-lookup"><span data-stu-id="d1fe7-138">You can't make calls to the Excel Services JavaScript object model from within a JavaScript UDF.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="d1fe7-139">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d1fe7-139">Additional resources</span></span>
<span data-ttu-id="d1fe7-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d1fe7-140"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="d1fe7-141">Службы Excel в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1fe7-141">Excel Services in SharePoint</span></span>](excel-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d1fe7-142">Новые возможности служб Excel для разработчиков</span><span class="sxs-lookup"><span data-stu-id="d1fe7-142">What's new in Excel Services for developers</span></span>](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [<span data-ttu-id="d1fe7-143">Пользовательские функции служб Excel</span><span class="sxs-lookup"><span data-stu-id="d1fe7-143">Excel Services User-Defined Functions</span></span>](http://msdn.microsoft.com/ru-ru/library/ms493934)
    
  

