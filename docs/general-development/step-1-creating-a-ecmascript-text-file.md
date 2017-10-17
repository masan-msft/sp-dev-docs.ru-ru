---
title: "Этап 1 Создание ECMAScript текстового файла"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1c2b359-5b0d-467d-a863-6732e23863b9
ms.openlocfilehash: b77d09f9aded3cd5dfca8c76413be8139fce1714
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-1-creating-a-ecmascript-text-file"></a>Этап 1: Создание ECMAScript текстового файла

Для этого пошагового руководства создается текстовый файл ECMAScript (JavaScript, JScript) . В этом пошаговом руководстве предполагается, что вы знакомы с написания кода в JavaScript. 
  
    
    


### <a name="to-create-an-ecmascript-text-file"></a>Для создания текстового файла в ECMAScript


1. Создайте текстовый файл и присвойте ему имя JSOM_FeedToContentEditor.txt.
    
  
2. Добавьте следующий скрипт в файл JSOM_FeedToContentEditor.txt.
    
    **Пример кода предоставлен:** Joshi Видия, корпорация Майкрософт.
    


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

3. Сохраните текстовый файл.
    
  

### <a name="to-save-the-text-file-to-a-trusted-document-library"></a>Для сохранения текстового файла в библиотеке надежных документов


1. Отправка текстового файла, созданного в предыдущей процедуре, надежная библиотека документов SharePoint. 
    
  
2. Обратите внимание, URL-адрес в текстовом файле. Например:
    
     `http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`
    
    В следующей процедуре необходимо будет этот URL-адрес для веб-канала в веб-часть редактора содержимого.
    
  

