---
title: "Используйте асинхронный вызов метода CloseWorkbook"
ms.date: 09/25/2017
keywords: async,how to,howdoi,howto
f1_keywords: async,how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 6febe7dc-a552-4c79-aa3e-203d882286e3
ms.openlocfilehash: 4abef18cee1d669291381a49c1d3b03d60db6da6
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="use-the-closeworkbook-method-call-asynchronously"></a>Используйте асинхронный вызов метода CloseWorkbook

When you are using Веб-службы Excel, it is good practice to close the workbook by calling the **CloseWorkbook** method if you are finished using the session. This closes the session and allows Службы Excel to free resources in a predictable manner. This could potentially improve your server performance and robustness.
  
    
    

However, any Web service call takes time. Depending on the way your server is installed, the way that you access it, and how much stress the server is under, the call can take anywhere between 50 milliseconds to 500 milliseconds. It can also take longer, but only if your server is under severe stress. Because a failed **CloseWorkbook** method call is not actionable, you do not need to wait for it to finish to see whether it succeeds. Because of this, you can usually make the call asynchronously and save some operation time.
  
    
    


> **Примечание:** Если приложение вызывает некоторые службы Excel и затем завершается, можно закрыть книгу синхронно, а не асинхронно. В этом случае вызове метода **CloseWorkbook** вместо метода **CloseWorkbookAsync** . Причиной является при выходе процесс сразу же после выдачи асинхронный вызов есть большая вероятность, вызов не может получить с помощью.
  
    
    

To close the workbook asynchronously, you must do two things:
- Make sure you do not dispose the Веб-службы Excel proxy classif you do, non-Службы Excel exceptions may occur. 
    
  
- Call the **CloseWorkbookAsync** method instead of the **CloseWorkbook** method. The signature for the **CloseWorkbookAsync** method is:
    
```
  
public void CloseWorkbookAsync(string sessionId)
```


```VB.net
  Public Sub CloseWorkbookAsync(ByVal sessionId As String)
End Sub
```

You don't have to implement the event that is called when the **CloseWorkbookAsync** method is called.You can find the signature in the "Reference.cs" file in your project "Web References" directory. 
> **Примечание:** Метод **CloseWorkbookAsync** можно найти в прокси-класса, созданного при добавлении веб-ссылки, с помощью Microsoft Visual Studio 2005. Если вы используете Visual Studio 2003, вызове метода **begincloseworkbook рабочая** Закрытие книги вместо асинхронно.
  
    
    

Calling the **CloseWorkbookAsync** method or **BeginCloseWorkbook** method means the call to close a workbook will be executed asynchronously and not cost your application any significant amount of time.
## <a name="example"></a>Пример

The following example shows how to close a workbook asynchronously using Visual Studio 2005.
  
    
    

```cs

using System;
using SampleApplication.ExcelWebService;
using System.Web.Services.Protocols;
namespace SampleApplication
{
    class Class1
    {
        [STAThread]
        static void Main(string[] args)
        {            
            // Instantiate the Web service 
            // and create a status array object.
            ExcelService es = new ExcelService();
            Status[] outStatus;

            string sheetName = "Sheet1";
            // TODO: change the workbook path to 
            // point to workbook in a trusted location
            // that you have access to. 
            string targetWorkbookPath = 
             "http://myserver02/example/Shared%20Documents/Book1.xlsx";

            // Set credentials for requests.
            es.Credentials = 
                System.Net.CredentialCache.DefaultCredentials;
            
            try
            {
                // Call open workbook, and point to the trusted   
                // location of the workbook to open.
                string sessionId = es.OpenWorkbook(targetWorkbookPath, 
                    "en-US", "en-US", out outStatus);
                // Call the GetCell method 
                // to retrieve a value from a cell.
                // The cell is in the first row and ninth column.
                object[] rangeResult2 = xlservice.GetCell(sessionId, 
                    sheetName, 0, 8, false, out outStatus);
 
                // Close the workbook asynchronously. 
                // This also closes session.
                es.CloseWorkbookAsync(sessionId);
            }
            catch (SoapException e)
            {
                Console.WriteLine("SOAP Exception Message: {0}", 
                   e.Message);
                Console.WriteLine("SOAP Exception Error Code: {0}", 
                   e.SubCode.Code.Name);
            }
            catch (Exception e)
            {
                Console.WriteLine("Exception Message: {0}", e.Message);
            }
            // Console.ReadLine();
        }
    }
}
 
```


```VB.net

Imports System
Imports SampleApplication.ExcelWebService
Imports System.Web.Services.Protocols
Namespace SampleApplication
    Friend Class Class1
        <STAThread> _
        Shared Sub Main(ByVal args() As String)
            ' Instantiate the Web service 
            ' and create a status array object.
            Dim es As New ExcelService()
            Dim outStatus() As Status

            Dim sheetName As String = "Sheet1"
            ' TODO: change the workbook path to 
            ' point to workbook in a trusted location
            ' that you have access to. 
            Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"

            ' Set credentials for requests.
            es.Credentials = System.Net.CredentialCache.DefaultCredentials

            Try
                ' Call open workbook, and point to the trusted   
                ' location of the workbook to open.
                Dim sessionId As String = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
                ' Call the GetCell method 
                ' to retrieve a value from a cell.
                ' The cell is in the first row and ninth column.
                Dim rangeResult2() As Object = xlservice.GetCell(sessionId, sheetName, 0, 8, False, outStatus)

                ' Close the workbook asynchronously. 
                ' This also closes session.
                es.CloseWorkbookAsync(sessionId)
            Catch e As SoapException
                Console.WriteLine("SOAP Exception Message: {0}", e.Message)
                Console.WriteLine("SOAP Exception Error Code: {0}", e.SubCode.Code.Name)
            Catch e As Exception
                Console.WriteLine("Exception Message: {0}", e.Message)
            End Try
            ' Console.ReadLine();
        End Sub
    End Class
End Namespace
```


## <a name="robust-programming"></a>Надежное программирование

Make sure that you add a Web reference to an Веб-службы Excel site that you have access to. Change the  `using SampleApplication.ExcelWebService;` statement to point to the Web service site that you are referencing.
  
    
    
In addition, make changes to the workbook path, sheet name, and so on, as appropriate.
  
    
    

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [How to: Catch Exceptions](how-to-catch-exceptions.md)
  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
  
    
    
 [How to: Save from Excel Client to the Server](how-to-save-from-excel-client-to-the-server.md)
  
    
    
 [How to: Use the SubCode Property to Capture Error Codes](how-to-use-the-subcode-property-to-capture-error-codes.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
