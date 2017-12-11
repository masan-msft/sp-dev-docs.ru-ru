---
title: "Асинхронный вызов метода CloseWorkbook"
ms.date: 09/25/2017
keywords: async,how to,howdoi,howto
f1_keywords: async,how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 6febe7dc-a552-4c79-aa3e-203d882286e3
ms.openlocfilehash: 7720c0d18c101d137906f217e5caf58f3ba6b7d0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-the-closeworkbook-method-call-asynchronously"></a><span data-ttu-id="19e60-103">Асинхронный вызов метода CloseWorkbook</span><span class="sxs-lookup"><span data-stu-id="19e60-103">Use the CloseWorkbook method call asynchronously</span></span>

<span data-ttu-id="19e60-p101">When you are using Веб-службы Excel, it is good practice to close the workbook by calling the **CloseWorkbook** method if you are finished using the session. This closes the session and allows Службы Excel to free resources in a predictable manner. This could potentially improve your server performance and robustness.</span><span class="sxs-lookup"><span data-stu-id="19e60-p101">When you are using Excel Web Services, it is good practice to close the workbook by calling the **CloseWorkbook** method if you are finished using the session. This closes the session and allows Excel Services to free resources in a predictable manner. This could potentially improve your server performance and robustness.</span></span>
  
    
    

<span data-ttu-id="19e60-p102">However, any Web service call takes time. Depending on the way your server is installed, the way that you access it, and how much stress the server is under, the call can take anywhere between 50 milliseconds to 500 milliseconds. It can also take longer, but only if your server is under severe stress. Because a failed **CloseWorkbook** method call is not actionable, you do not need to wait for it to finish to see whether it succeeds. Because of this, you can usually make the call asynchronously and save some operation time.</span><span class="sxs-lookup"><span data-stu-id="19e60-p102">However, any Web service call takes time. Depending on the way your server is installed, the way that you access it, and how much stress the server is under, the call can take anywhere between 50 milliseconds to 500 milliseconds. It can also take longer, but only if your server is under severe stress. Because a failed **CloseWorkbook** method call is not actionable, you do not need to wait for it to finish to see whether it succeeds. Because of this, you can usually make the call asynchronously and save some operation time.</span></span>
  
> [!NOTE]
> <span data-ttu-id="19e60-p103">[!Примечание] If your application makes some calls to Службы Excel and then exits, you may want to close a workbook synchronously instead of asynchronously. In this case, you call the **CloseWorkbook** method instead of the **CloseWorkbookAsync** method. The reason is if you immediately exit the process after issuing an asynchronous call, there is a good chance the call might not get through.</span><span class="sxs-lookup"><span data-stu-id="19e60-p103">If your application makes some calls to Excel Services and then exits, you may want to close a workbook synchronously instead of asynchronously. In this case, you call the **CloseWorkbook** method instead of the **CloseWorkbookAsync** method. The reason is if you immediately exit the process after issuing an asynchronous call, there is a good chance the call might not get through.</span></span>
  
    
    

<span data-ttu-id="19e60-115">To close the workbook asynchronously, you must do two things:</span><span class="sxs-lookup"><span data-stu-id="19e60-115">To close the workbook asynchronously, you must do two things:</span></span>
- <span data-ttu-id="19e60-116">Make sure you do not dispose the Веб-службы Excel proxy classif you do, non-Службы Excel exceptions may occur.</span><span class="sxs-lookup"><span data-stu-id="19e60-116">Make sure you do not dispose the Excel Web Services proxy class—if you do, non-Excel Services exceptions may occur.</span></span> 
    
  
- <span data-ttu-id="19e60-p104">Call the **CloseWorkbookAsync** method instead of the **CloseWorkbook** method. The signature for the **CloseWorkbookAsync** method is:</span><span class="sxs-lookup"><span data-stu-id="19e60-p104">Call the **CloseWorkbookAsync** method instead of the **CloseWorkbook** method. The signature for the **CloseWorkbookAsync** method is:</span></span>
    
```
  
public void CloseWorkbookAsync(string sessionId)
```


```VB.net
  Public Sub CloseWorkbookAsync(ByVal sessionId As String)
End Sub
```

<span data-ttu-id="19e60-119">You don't have to implement the event that is called when the **CloseWorkbookAsync** method is called.You can find the signature in the "Reference.cs" file in your project "Web References" directory.</span><span class="sxs-lookup"><span data-stu-id="19e60-119">You don't have to implement the event that is called when the **CloseWorkbookAsync** method is called.You can find the signature in the "Reference.cs" file in your project "Web References" directory.</span></span> 

> [!NOTE]
> <span data-ttu-id="19e60-p105">[!Примечание] You can find the **CloseWorkbookAsync** method in the proxy class that is generated when you add a Web reference using Microsoft Visual Studio 2005. If you are using Visual Studio 2003, you call the **BeginCloseWorkbook** method to close a workbook asynchronously instead.</span><span class="sxs-lookup"><span data-stu-id="19e60-p105">You can find the **CloseWorkbookAsync** method in the proxy class that is generated when you add a Web reference using Microsoft Visual Studio 2005. If you are using Visual Studio 2003, you call the **BeginCloseWorkbook** method to close a workbook asynchronously instead.</span></span>
  
    
    

<span data-ttu-id="19e60-122">Calling the **CloseWorkbookAsync** method or **BeginCloseWorkbook** method means the call to close a workbook will be executed asynchronously and not cost your application any significant amount of time.</span><span class="sxs-lookup"><span data-stu-id="19e60-122">Calling the **CloseWorkbookAsync** method or **BeginCloseWorkbook** method means the call to close a workbook will be executed asynchronously and not cost your application any significant amount of time.</span></span>
## <a name="example"></a><span data-ttu-id="19e60-123">Пример</span><span class="sxs-lookup"><span data-stu-id="19e60-123">Example</span></span>

<span data-ttu-id="19e60-124">The following example shows how to close a workbook asynchronously using Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="19e60-124">The following example shows how to close a workbook asynchronously using Visual Studio 2005.</span></span>
  
    
    

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


## <a name="robust-programming"></a><span data-ttu-id="19e60-125">Надежное программирование</span><span class="sxs-lookup"><span data-stu-id="19e60-125">Robust programming</span></span>

<span data-ttu-id="19e60-p106">Make sure that you add a Web reference to an Веб-службы Excel site that you have access to. Change the  `using SampleApplication.ExcelWebService;` statement to point to the Web service site that you are referencing.</span><span class="sxs-lookup"><span data-stu-id="19e60-p106">Make sure that you add a Web reference to an Excel Web Services site that you have access to. Change the  `using SampleApplication.ExcelWebService;` statement to point to the Web service site that you are referencing.</span></span>
  
    
    
<span data-ttu-id="19e60-128">In addition, make changes to the workbook path, sheet name, and so on, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="19e60-128">In addition, make changes to the workbook path, sheet name, and so on, as appropriate.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="19e60-129">См. также</span><span class="sxs-lookup"><span data-stu-id="19e60-129">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="19e60-130">Задачи</span><span class="sxs-lookup"><span data-stu-id="19e60-130">Tasks</span></span>


  
    
    
 [<span data-ttu-id="19e60-131">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="19e60-131">How to: Catch Exceptions</span></span>](how-to-catch-exceptions.md)
  
    
    
 [<span data-ttu-id="19e60-132">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="19e60-132">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="19e60-133">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="19e60-133">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
  
    
    
 [<span data-ttu-id="19e60-134">How to: Use the SubCode Property to Capture Error Codes</span><span class="sxs-lookup"><span data-stu-id="19e60-134">How to: Use the SubCode Property to Capture Error Codes</span></span>](how-to-use-the-subcode-property-to-capture-error-codes.md)
#### <a name="concepts"></a><span data-ttu-id="19e60-135">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="19e60-135">Concepts</span></span>


  
    
    
 [<span data-ttu-id="19e60-136">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="19e60-136">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="19e60-137">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="19e60-137">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="19e60-138">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="19e60-138">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="19e60-139">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="19e60-139">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="19e60-140">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="19e60-140">Other resources</span></span>


  
    
    
 [<span data-ttu-id="19e60-141">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="19e60-141">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
