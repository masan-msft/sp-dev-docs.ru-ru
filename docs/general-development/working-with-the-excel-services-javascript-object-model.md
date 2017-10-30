---
title: "Работа с моделью объектов JavaScript службы Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 06219071-a7c1-4f54-b07f-7b7001592330
ms.openlocfilehash: 9bf873dad64b0dedc3d4676646594d70ec3815a7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-the-excel-services-javascript-object-model"></a>Работа с моделью объектов JavaScript службы Excel

При написании кода, который использует объектную модель JavaScript (JSOM), существует два сценария, где код может выполняться: на странице SharePoint; или на веб-страницу узла, который содержит внедренной книги, которые хранятся на Microsoft OneDrive. В этой статье описывается основное различие между двумя сценарии, которые значительно повлиять на написание кода.
  
    
    


## <a name="using-the-excel-services-jsom"></a>С помощью служб Excel JSOM

В таблице 1 перечислены различия между два сценария, доступные при создании кода, который использует JSOM.
  
    
    

**В таблице 1. Сценарии для служб Excel JSOM**


|**Расположение**|**Описание**|
|:-----|:-----|
|**OneDrive** <br/> |В этом сценарии внедрение книги, которые хранятся на OneDrive в веб-узла, с помощью HTML <div> элемент. Затем включить код на странице, взаимодействующий с внедренной книги.  <br/> |
|**SharePoint** <br/> |В этом сценарии у вас есть на странице SharePoint, удовлетворить с помощью SharePoint. Вставка веб-части на страницу SharePoint, содержащий книгу, которая хранится в надежном расположении. Затем включить код на странице SharePoint, который взаимодействует с веб-части.  <br/> |
   
Основное различие между написания кода для двух сценариев  это, как получить ссылку на объект  [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx) . Поскольку **[Ewa.EwaControl]** точка входа в объектной модели JavaScript , необходимо получить ссылку на него для работы с JSOM.
  
    
    

### <a name="getting-a-reference-to-the-ewacontrol-object-sharepoint"></a>Получение ссылки на объект EwaControl (SharePoint)

При создании кода, который взаимодействует с веб-части на страницу SharePoint, как показано в следующем примере кода вы получите ссылку на объект **[Ewa.EwaControl]** с помощью метода [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx).
  
    
    

```

<script type="text/javascript">
var ewa = null;

// Add event handler for onload event.
if (window.attachEvent) 
{ 
    window.attachEvent("onload", ewaOmPageLoad);    
} 
else 
{ 
    window.addEventListener("DOMContentLoaded", ewaOmPageLoad, false); 
}
// Add event handler for applicationReady event.
function ewaOnPageLoad()
{
    if (typeof (Ewa) != "undefined")
    {
Ewa.EwaControl.add_applicationReady(ewaApplicationReady);
    }
    else
    {
alert("Error - the EWA is not loaded.");
    }
    // Add additional page load code here.
}

function ewaApplicationReady()
{
    // Get a reference to the Excel Services Web Part.
    ewa = Ewa.EwaControl.getInstances().getItem(0);

    // Add other initialization logic here.
}

// Add your code here.
    </script>
```


### <a name="getting-a-reference-to-the-ewacontrol-object-onedrive"></a>Получение ссылки на объект EwaControl (OneDrive )

При создании кода, который взаимодействует с внедренной книги, которые хранятся на OneDrive, вы получите ссылку на объект **[Ewa.EwaControl]** через объект [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx) . Объект **[AsyncResult]** передается в качестве единственного параметра метод обратного вызова, указанные в статический метод [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) . При вызове функции обратного вызова, ссылку на объект **[Ewa.EwaControl]** содержатся в объекте **[AsyncResult]**. В следующем примере кода показано, как получить ссылку на объект **[Ewa.EwaControl]** через объект **[AsyncResult]**.
  
    
    

```

<div id="myExcelDiv" style="width: 402px; height: 346px"></div>
<script type="text/javascript" src="http://r.office.microsoft.com/r/rlidExcelWLJS?v=1&amp;kip=1"></script>
<script type="text/javascript">
    /*
    * This code uses the Microsoft Office Excel JavaScript object model to programmatically insert the
    * Excel Web App into a div with id=myExcelDiv. The full API is documented at
    * http://msdn.microsoft.com/en-us/library/hh315812.aspx. There you can find out how to programmatically get
    * values from your Excel file and how to use the rest of the object model. 
    */

    // Use this file token to reference Book1.xlsx in the Excel APIs
    // Replace the the placeholder for the  filetoken with your value
    var fileToken = " XXXXXXXXXXXXXXXXXXXXXX/XXXXXXXXXXXXXXXXXXX/";
    var ewa = null;

    // Run the Excel load handler on page load.
    if (window.attachEvent)
    {
        window.attachEvent("onload", loadEwaOnPageLoad);
    } else
    {
        window.addEventListener("DOMContentLoaded", loadEwaOnPageLoad, false);
    }

    function loadEwaOnPageLoad()
    {
        var props = {
            uiOptions: {
                showGridlines: false,
                showRowColumnHeaders: false,
                showParametersTaskPane: false
            },
            interactivityOptions: {
                allowTypingAndFormulaEntry: false,
                allowParameterModification: false,
                allowSorting: false,
                allowFiltering: false,
                allowPivotTableInteractivity: false
            }
        };
        // Embed workbook using loadEwaAsync
        Ewa.EwaControl.loadEwaAsync(fileToken, "myExcelDiv", props, onEwaLoaded);
    }

    function onEwaLoaded(asyncResult)
    { 
        if (asyncResult.getSucceeded())
        {
            // Use the AsyncResult.getEwaControl() method to get a reference to the EwaControl object
            ewa = asyncResult.getEwaControl();
            …
        }
        else
        {
            alert("Async operation failed!");
        }
        // ...
    }    
</script>
```


### <a name="conclusion"></a>Заключение

Написание решение, с помощью объектной модели JavaScript —? практически ли решение запускается на SharePoint или на веб-страницу узла. Основное различие заключается в том, как получить ссылку на объект **[Ewa.EwaControl]** . После получения ссылки на объект **[Ewa.EwaControl]** rest код, который будет схожих для обоих сценариев.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15DevKitchenCon_AnatomyofanappSignupsheets_Additionalresources"> </a>


-  [С помощью API JavaScript служб Excel для работы с внедренными книгами Excel](http://msdn.microsoft.com/en-us/library/hh315812.aspx)
    
  
-  [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx)
    
  
-  [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx)
    
  

