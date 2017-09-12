---
title: "Обзор ECMAScript служб Excel"
ms.prod: OFFICE365
ms.assetid: f8c1be86-df19-44c3-a3bc-c0da2b80df10
ms.openlocfilehash: 159464b1ad0e125b8cf5905db039871d53515ccf
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="excel-services-ecmascript-overview"></a>Обзор ECMAScript служб Excel

In Microsoft SharePoint Server 2010, Службы Excel added support for ECMAScript (JavaScript, JScript). JavaScript enables a new set of solutions by using Службы Excel. 
  
    
    

The JavaScript object model in Службы Excel enables developers to automate, customize, and interact with the Веб-клиент Excel Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Веб-клиент Excel Web Part controls on a page. It also enables you to add more capabilities to your workbooks and to code around them. By using the JavaScript object model, it is possible to detect and react to a user's interactions with an Веб-клиент Excel Web Part and to programmatically interact with one or multiple Веб-клиент Excel Web Parts.
  
    
    


## <a name="using-the-ecmascript-object-model"></a>Using the ECMAScript Object Model

To use the JavaScript object model in Службы Excel, you insert the JavaScript code on the page that contains the Веб-клиент Excel Web Part. This can be done by adding the code to the Web Part page by using the Content Editor Web Part or by directly editing the .aspx page.
  
    
    
The JavaScript object model in Службы Excel enables developers to: 
  
    
    

- Access items in a workbook such as ranges, tables, PivotTables, charts, and sheets.
    
  
- Set and retrieve values from cells by using ranges or named ranges.
    
  
- Raise events when the user changes the active selection or active cell or when the user starts editing a cell.
    
  
- Scroll to a different region and to switch the displayed sheet or named item. 
    
  
Дополнительные сведения см. по следующим ссылкам:
  
    
    

- For more information about the JavaScript object model in Службы Excel, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.
    
  
- For an example of how to interact with the JavaScript object model in Службы Excel by using the Content Editor Web Part, see  [Пошаговое руководство по разработке с использованием веб-части редактора контента](walkthrough-developing-using-the-content-editor-web-part).
    
  

## <a name="ecmascript-js-file-location"></a>ECMAScript .js File Location

Minified .js files for the JavaScript object model are installed in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS directory. The name of the file is EwaMoss.js.
  
    
    
For basic information about how to use the JavaScript object model within an .aspx page or .js file, see  [Настройка страницы приложения для ECMAScript](http://msdn.microsoft.com/library/48582a0b-f787-4868-8298-958717ec8ff8%28Office.15%29.aspx).
  
    
    

