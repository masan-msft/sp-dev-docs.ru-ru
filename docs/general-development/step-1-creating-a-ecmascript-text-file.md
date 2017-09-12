---
title: "Этап 1 Создание ECMAScript текстового файла"
ms.prod: OFFICE365
ms.assetid: f1c2b359-5b0d-467d-a863-6732e23863b9
ms.openlocfilehash: 5fd205524ee384fc8d90b5908804a9166e4f9ffd
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="step-1-creating-a-ecmascript-text-file"></a><span data-ttu-id="20955-102">Этап 1: Создание ECMAScript текстового файла</span><span class="sxs-lookup"><span data-stu-id="20955-102">Step 1: Creating a ECMAScript Text File</span></span>

<span data-ttu-id="20955-p101">Для этого пошагового руководства создается текстовый файл ECMAScript (JavaScript, JScript) . В этом пошаговом руководстве предполагается, что вы знакомы с написания кода в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="20955-p101">For this walkthrough, you will create an ECMAScript (JavaScript, JScript) text file. This walkthrough assumes that you are familiar with coding in JavaScript.</span></span> 
  
    
    


### <a name="to-create-an-ecmascript-text-file"></a><span data-ttu-id="20955-105">Для создания текстового файла в ECMAScript</span><span class="sxs-lookup"><span data-stu-id="20955-105">To create an ECMAScript text file</span></span>


1. <span data-ttu-id="20955-106">Создайте текстовый файл и присвойте ему имя JSOM_FeedToContentEditor.txt.</span><span class="sxs-lookup"><span data-stu-id="20955-106">Create a text file and name it JSOM_FeedToContentEditor.txt.</span></span>
    
  
2. <span data-ttu-id="20955-107">Добавьте следующий скрипт в файл JSOM_FeedToContentEditor.txt.</span><span class="sxs-lookup"><span data-stu-id="20955-107">Add the following script to the JSOM_FeedToContentEditor.txt file.</span></span>
    
    <span data-ttu-id="20955-108">**Пример кода предоставлен:** Joshi Видия, корпорация Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="20955-108">**Sample code provided by:** Vidya Joshi, Microsoft Corporation.</span></span>
    


```
  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
 <head>Logging results:
 </head>
<body>
<div id='resultdiv'></div>
<script type="text/javascript">         

// Set the page event handlers for onload and unload.
if (window.attachEvent) 
{
    window.attachEvent("onload", Page_Load);
} 
else 
{
// For some browsers window.attachEvent does not exist.
    window.addEventListener("DOMContentLoaded", Page_Load, false);
}

// Load the page. 
function Page_Load() 
{
    Ewa.EwaControl.add_applicationReady(GetEwa);
}

function GetEwa()
{
    om =Ewa.EwaControl.getInstances().getItem(0);
    writelog('DomId:' + om.getDomElement().id,0);

    om.add_activeCellChanged(cellchanged);
    om.add_activeSelectionChanged(selChanged);
    om.add_gridSynchronized(gridSynchronized);
    om.add_workbookChanged(wbchanged);
    om.add_enteredCellEditing(editing);
}

function cellchanged(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Cell changed event triggered',0);
}

function selChanged(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Selection changed event triggered',0);
}

function gridSynchronized(res)
{
    writelog('WorkbookPath:' +om.getActiveWorkbook().getWorkbookPath(),1);
    writelog('grid synchronized',0);
}

function wbchanged(r)
{
    writelog('Workbook changed event triggered',0);
}

function editing(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Entered cell editing event triggered',0);
}

function writelog(output, indentLevel)
{
    output = output + "<br/>";
    document.getElementById('resultdiv').innerHTML = output + document.getElementById('resultdiv').innerHTML ;
}
</script>  
</body>
</html><html> 

```

3. <span data-ttu-id="20955-109">Сохраните текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="20955-109">Save the text file.</span></span>
    
  

### <a name="to-save-the-text-file-to-a-trusted-document-library"></a><span data-ttu-id="20955-110">Для сохранения текстового файла в библиотеке надежных документов</span><span class="sxs-lookup"><span data-stu-id="20955-110">To save the text file to a trusted document library</span></span>


1. <span data-ttu-id="20955-111">Отправка текстового файла, созданного в предыдущей процедуре, надежная библиотека документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="20955-111">Upload the text file that you created in the previous procedure to a trusted SharePoint document library.</span></span> 
    
  
2. <span data-ttu-id="20955-p102">Обратите внимание, URL-адрес в текстовом файле. Например:</span><span class="sxs-lookup"><span data-stu-id="20955-p102">Note the URL to the text file. For example:</span></span>
    
     <span data-ttu-id="20955-114">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span><span class="sxs-lookup"><span data-stu-id="20955-114">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span></span>
    
    <span data-ttu-id="20955-115">В следующей процедуре необходимо будет этот URL-адрес для веб-канала в веб-часть редактора содержимого.</span><span class="sxs-lookup"><span data-stu-id="20955-115">In the next procedure, you will need this URL to feed to the Content Editor Web Part.</span></span>
    
  

