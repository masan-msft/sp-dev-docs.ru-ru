---
title: "Петлевые и вызовы с использованием SOAP и прямые вызовы"
ms.prod: OFFICE365
ms.assetid: bffc6565-636f-40d4-ba17-2511070ba5db
ms.openlocfilehash: fad0976c763575ebbe0357d93132c6bb5b7459b6
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="loop-back-soap-calls-and-direct-linking"></a>Петлевые и вызовы с использованием SOAP и прямые вызовы

If you are writing code within Microsoft SharePoint Foundation, for example, a custom Web Part, custom aspx page, and so on, you should make direct calls to Microsoft.Office.Excel.Server.WebServices.dll. You do this by linking directly to Microsoft.Office.Excel.Server.WebServices.dll. 
  
    
    

Using Simple Object Access Protocol (SOAP) from a Web server to communicate with the same Web server is also known as using loop-back SOAP calls. It is strongly recommended that you do not attempt to use loop-back SOAP calls. If you are writing code within SharePoint Foundation, you should not use SOAP to call the Веб-службы Excel. You should instead link to Microsoft.Office.Excel.Server.WebServices.dll locally and make calls to it as you would any local assembly.
## <a name="location-of-microsoftofficeexcelserverwebservicesdll"></a>Location of Microsoft.Office.Excel.Server.WebServices.dll

You can find Microsoft.Office.Excel.Server.WebServices.dll in one of the following locations:
  
    
    

-  _[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI
    
  
- Global assembly cache 
    
  

## <a name="adding-a-reference-to-microsoftofficeexcelserverwebservicesdll"></a>Adding a Reference to Microsoft.Office.Excel.Server.WebServices.dll

To link directly to Microsoft.Office.Excel.Server.WebServices.dll in your project and call it from your code, you add a reference to it. On the computer where you have installed Microsoft SharePoint Server 2010, using the **Add Reference** dialog box in Microsoft Visual Studio, you can do one of the following:
  
    
    

- Select **Excel Web Services** from the **Component Name** list in the **.NET** tab.
    
  
- Browse to Microsoft.Office.Excel.Server.WebServices.dll located in:
  
    
    
 _[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI
    
  

## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips)
  
    
    
 [Excel Services Alerts](excel-services-alerts)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services)
