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
# <a name="working-with-the-excel-services-javascript-object-model"></a><span data-ttu-id="b8811-102">Работа с моделью объектов JavaScript службы Excel</span><span class="sxs-lookup"><span data-stu-id="b8811-102">Working with the Excel Services JavaScript object model</span></span>

<span data-ttu-id="b8811-103">При написании кода, который использует объектную модель JavaScript (JSOM), существует два сценария, где код может выполняться: на странице SharePoint; или на веб-страницу узла, который содержит внедренной книги, которые хранятся на Microsoft OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b8811-103">When you write code that uses the JavaScript object model (JSOM), there are two scenarios where the code can run: on a SharePoint page; or on a host webpage that contains an embedded workbook that is stored on Microsoft OneDrive.</span></span> <span data-ttu-id="b8811-104">В этой статье описывается основное различие между двумя сценарии, которые значительно повлиять на написание кода.</span><span class="sxs-lookup"><span data-stu-id="b8811-104">This article discusses the main difference between the two scenarios that significantly affect how you write your code.</span></span>
  
    
    


## <a name="using-the-excel-services-jsom"></a><span data-ttu-id="b8811-105">С помощью служб Excel JSOM</span><span class="sxs-lookup"><span data-stu-id="b8811-105">Using the Excel Services JSOM</span></span>

<span data-ttu-id="b8811-106">В таблице 1 перечислены различия между два сценария, доступные при создании кода, который использует JSOM.</span><span class="sxs-lookup"><span data-stu-id="b8811-106">Table 1 lists the difference between the two scenarios available when you write code that uses the JSOM.</span></span>
  
    
    

<span data-ttu-id="b8811-107">**В таблице 1. Сценарии для служб Excel JSOM**</span><span class="sxs-lookup"><span data-stu-id="b8811-107">**Table 1. Scenarios for Excel Services JSOM**</span></span>


|<span data-ttu-id="b8811-108">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="b8811-108">**Location**</span></span>|<span data-ttu-id="b8811-109">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b8811-109">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b8811-110">**OneDrive**</span><span class="sxs-lookup"><span data-stu-id="b8811-110">**OneDrive**</span></span> <br/> |<span data-ttu-id="b8811-111">В этом сценарии внедрение книги, которые хранятся на OneDrive в веб-узла, с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="b8811-111">In this scenario, you embed a workbook that is stored on OneDrive into the host webpage using an HTML</span></span> <div> <span data-ttu-id="b8811-112">элемент.</span><span class="sxs-lookup"><span data-stu-id="b8811-112">element.</span></span> <span data-ttu-id="b8811-113">Затем включить код на странице, взаимодействующий с внедренной книги.</span><span class="sxs-lookup"><span data-stu-id="b8811-113">Then you include code in the page that interacts with the embedded workbook.</span></span>  <br/> |
|<span data-ttu-id="b8811-114">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="b8811-114">**SharePoint**</span></span> <br/> |<span data-ttu-id="b8811-115">В этом сценарии у вас есть на странице SharePoint, удовлетворить с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8811-115">In this scenario, you have a SharePoint page served by SharePoint.</span></span> <span data-ttu-id="b8811-116">Вставка веб-части на страницу SharePoint, содержащий книгу, которая хранится в надежном расположении.</span><span class="sxs-lookup"><span data-stu-id="b8811-116">You insert an Web Part into the SharePoint page that contains a workbook that is stored in an trusted location.</span></span> <span data-ttu-id="b8811-117">Затем включить код на странице SharePoint, который взаимодействует с веб-части.</span><span class="sxs-lookup"><span data-stu-id="b8811-117">Then you include code in the SharePoint page that interacts with the Web Part.</span></span>  <br/> |
   
<span data-ttu-id="b8811-p104">Основное различие между написания кода для двух сценариев  это, как получить ссылку на объект  [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx) . Поскольку **[Ewa.EwaControl]** точка входа в объектной модели JavaScript , необходимо получить ссылку на него для работы с JSOM.</span><span class="sxs-lookup"><span data-stu-id="b8811-p104">The main difference between writing code for the two scenarios is how you get a reference to the  [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx) object. Because the **[Ewa.EwaControl]** is the entry point to the JavaScript object model, you must get a reference to it to work with the JSOM.</span></span>
  
    
    

### <a name="getting-a-reference-to-the-ewacontrol-object-sharepoint"></a><span data-ttu-id="b8811-120">Получение ссылки на объект EwaControl (SharePoint)</span><span class="sxs-lookup"><span data-stu-id="b8811-120">Getting a reference to the EwaControl object (SharePoint)</span></span>

<span data-ttu-id="b8811-121">При создании кода, который взаимодействует с веб-части на страницу SharePoint, как показано в следующем примере кода вы получите ссылку на объект **[Ewa.EwaControl]** с помощью метода [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8811-121">When writing code that interacts with an Web Part on a SharePoint page, you get a reference to the **[Ewa.EwaControl]** object by using the method, [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx), as shown in the following code example.</span></span>
  
    
    

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


### <a name="getting-a-reference-to-the-ewacontrol-object-onedrive"></a><span data-ttu-id="b8811-122">Получение ссылки на объект EwaControl (OneDrive )</span><span class="sxs-lookup"><span data-stu-id="b8811-122">Getting a reference to the EwaControl object (OneDrive)</span></span>

<span data-ttu-id="b8811-p105">При создании кода, который взаимодействует с внедренной книги, которые хранятся на OneDrive, вы получите ссылку на объект **[Ewa.EwaControl]** через объект [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx) . Объект **[AsyncResult]** передается в качестве единственного параметра метод обратного вызова, указанные в статический метод [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) . При вызове функции обратного вызова, ссылку на объект **[Ewa.EwaControl]** содержатся в объекте **[AsyncResult]**. В следующем примере кода показано, как получить ссылку на объект **[Ewa.EwaControl]** через объект **[AsyncResult]**.</span><span class="sxs-lookup"><span data-stu-id="b8811-p105">When writing code that interacts with an embedded workbook that is stored on OneDrive, you get a reference to the **[Ewa.EwaControl]** object through the [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx) object. The **[AsyncResult]** object is passed in as the single parameter to the callback method that you specify in the [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) static method. When the callback is invoked, a reference to the **[Ewa.EwaControl]** object is included in the **[AsyncResult]** object. The following code example shows how you get a reference to the **[Ewa.EwaControl]** object through the **[AsyncResult]** object.</span></span>
  
    
    

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


### <a name="conclusion"></a><span data-ttu-id="b8811-127">Заключение</span><span class="sxs-lookup"><span data-stu-id="b8811-127">Conclusion</span></span>

<span data-ttu-id="b8811-128">Написание решение, с помощью объектной модели JavaScript —? практически ли решение запускается на SharePoint или на веб-страницу узла.</span><span class="sxs-lookup"><span data-stu-id="b8811-128">Writing a solution that uses the JavaScript object model is basically the same whether the solution runs on SharePoint or on a host webpage.</span></span> <span data-ttu-id="b8811-129">Основное различие заключается в том, как получить ссылку на объект **[Ewa.EwaControl]** .</span><span class="sxs-lookup"><span data-stu-id="b8811-129">The main difference is how you get a reference to the **[Ewa.EwaControl]** object.</span></span> <span data-ttu-id="b8811-130">После получения ссылки на объект **[Ewa.EwaControl]** rest код, который будет схожих для обоих сценариев.</span><span class="sxs-lookup"><span data-stu-id="b8811-130">Once you have a reference to the **[Ewa.EwaControl]** object, the rest of the code that you write will be almost the same for both scenarios.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="b8811-131">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b8811-131">Additional resources</span></span>
<span data-ttu-id="b8811-132"><a name="SP15DevKitchenCon_AnatomyofanappSignupsheets_Additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b8811-132"></span></span>


-  [<span data-ttu-id="b8811-133">С помощью API JavaScript служб Excel для работы с внедренными книгами Excel</span><span class="sxs-lookup"><span data-stu-id="b8811-133">Using the Excel Services JavaScript API to Work with Embedded Excel Workbooks</span></span>](http://msdn.microsoft.com/en-us/library/hh315812.aspx)
    
  
-  [<span data-ttu-id="b8811-134">Ewa.EwaControl.loadEwaAsync</span><span class="sxs-lookup"><span data-stu-id="b8811-134">Ewa.EwaControl.loadEwaAsync</span></span>](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="b8811-135">Ewa.EwaControlCollection.getItem(index)</span><span class="sxs-lookup"><span data-stu-id="b8811-135">Ewa.EwaControlCollection.getItem(index)</span></span>](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx)
    
  

