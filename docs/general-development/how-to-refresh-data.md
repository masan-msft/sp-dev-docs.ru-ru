---
title: "Обновление данных"
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 6cfd89ff-846e-486b-8f73-a109016813ab
ms.openlocfilehash: e20ec7f931b88605f7a8e888f8a1ea30b66ec1bb
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="refresh-data"></a><span data-ttu-id="75cee-103">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="75cee-103">Refresh data</span></span>

<span data-ttu-id="75cee-p101">This example shows how to retrieve updated data from external data sources for the open workbook by using the **Refresh** method. The Веб-службы Excel signature for the **Refresh** method is as follows:</span><span class="sxs-lookup"><span data-stu-id="75cee-p101">This example shows how to retrieve updated data from external data sources for the open workbook by using the **Refresh** method. The Excel Web Services signature for the **Refresh** method is as follows:</span></span>
  
    
    


```cs

public Status[] Refresh (string sessionId, string connectionName)
```


```VB.net
Public Function Refresh(ByVal sessionId As String, ByVal connectionName As String) As Status()
End Function
```

<span data-ttu-id="75cee-106">If you link directly to Microsoft.Office.Excel.Server.WebServices.dll, the signature for the **Refresh** method is:</span><span class="sxs-lookup"><span data-stu-id="75cee-106">If you link directly to Microsoft.Office.Excel.Server.WebServices.dll, the signature for the **Refresh** method is:</span></span>


```cs

public void Refresh (string sessionId, string connectionName,
    out Status[] status)
```




```VB.net

Public Sub Refresh(ByVal sessionId As String, ByVal connectionName As String, <System.Runtime.InteropServices.Out()> ByRef status() As Status)
End Sub
```

<span data-ttu-id="75cee-p102">The  `connectionName` argument refers to the connection name in a Microsoft Office Excel 2007 workbook.You can use the **Refresh** method to refresh a single data connection in the workbook, or to refresh all connections. This is useful particularly when the connections are created without refresh-on-open functionality.When you refresh a connection, the data and all objects using the connection will be refreshed. To refresh all available connections in the workbook, you pass in an empty connection string or **null** for the connection name argument.The refresh operations will be attempted regardless of the type of authentication used, without any further confirmation or prompt.For more information about the **Refresh** method, see the Веб-службы Excel reference documentation.</span><span class="sxs-lookup"><span data-stu-id="75cee-p102">The  `connectionName` argument refers to the connection name in a Microsoft Office Excel 2007 workbook.You can use the **Refresh** method to refresh a single data connection in the workbook, or to refresh all connections. This is useful particularly when the connections are created without refresh-on-open functionality.When you refresh a connection, the data and all objects using the connection will be refreshed. To refresh all available connections in the workbook, you pass in an empty connection string or **null** for the connection name argument.The refresh operations will be attempted regardless of the type of authentication used, without any further confirmation or prompt.For more information about the **Refresh** method, see the Excel Web Services reference documentation.</span></span>
## <a name="example"></a><span data-ttu-id="75cee-110">Пример</span><span class="sxs-lookup"><span data-stu-id="75cee-110">Example</span></span>

<span data-ttu-id="75cee-p103">The following code sample shows how to call the **Refresh** method using Веб-службы Excel. The connection name in this example is "MyInventoryConnection":</span><span class="sxs-lookup"><span data-stu-id="75cee-p103">The following code sample shows how to call the **Refresh** method using Excel Web Services. The connection name in this example is "MyInventoryConnection":</span></span>
  
    
    

```cs

// Instantiate the Web service.
ExcelService xlservice = new ExcelService();
Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
string sheetName = "Sheet3";

// Set the path to the workbook to open.
// TODO: Change the path to the workbook
// to point to a workbook you have access to.
// The workbook must be in a trusted location.
string targetWorkbookPath = 
    http://myserver02/example/Shared%20Documents/Book1.xlsx";
            
// Set credentials for requests.
xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials;

// Call open workbook, and point to the trusted   
// location of the workbook to open.
string sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);
 
// Prepare object to define range coordinates.
rangeCoordinates.Column = 0;
rangeCoordinates.Row = 0;
rangeCoordinates.Height = 8;
rangeCoordinates.Width = 10;

// Set the cell located in the first row and 
// ninth column to 300.
xlservice.SetCell(sessionId, sheetName, 0, 8, 300); 
xlservice.Refresh(sessionId, "MyInventoryConnection");
```


```VB.net

' Instantiate the Web service.
Dim xlservice As New ExcelService()
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
Dim sheetName As String = "Sheet3"

' Set the path to the workbook to open.
' TODO: Change the path to the workbook
' to point to a workbook you have access to.
' The workbook must be in a trusted location.
' Set credentials for requests.
Dim targetWorkbookPath As String = http: xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials 'myserver02/example/Shared%20Documents/Book1.xlsx";

' Call open workbook, and point to the trusted   
' location of the workbook to open.
Dim sessionId As String = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)

' Prepare object to define range coordinates.
rangeCoordinates.Column = 0
rangeCoordinates.Row = 0
rangeCoordinates.Height = 8
rangeCoordinates.Width = 10

' Set the cell located in the first row and 
' ninth column to 300.
xlservice.SetCell(sessionId, sheetName, 0, 8, 300)
xlservice.Refresh(sessionId, "MyInventoryConnection")
```

<span data-ttu-id="75cee-113">If you link directly to Microsoft.Office.Excel.Server.WebServices.dll, the equivalent code is:</span><span class="sxs-lookup"><span data-stu-id="75cee-113">If you link directly to Microsoft.Office.Excel.Server.WebServices.dll, the equivalent code is:</span></span>
  
    
    



```

// Instantiate the ExcelService class.
ExcelService xlservice = new ExcelService();
Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
string sheetName = "Sheet3";

// Set the path to the workbook to open.
// TODO: Change the path to the workbook
// to point to a workbook you have access to.
// The workbook must be in a trusted location.
string targetWorkbookPath = 
    http://myserver02/example/Shared%20Documents/Book1.xlsx";
            
// Call the open workbook, and point to the trusted 
// location of the workbook to open.
string sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);
                
// Set the cell located in the first row and 
// ninth column to 300.
xlservice.SetCell(sessionId, sheetName, 0, 8, 300, out outStatus); 
xlservice.Refresh(sessionId, "MyInventoryConnection", out outStatus);

byte[] workbook = xlService.GetWorkbook(sessionId, WorkbookType.FullWorkbook, out status);

// Write the resulting Excel file to stdout 
// as a binary stream.
BinaryWriter binaryWriter = 
    new BinaryWriter(Console.OpenStandardOutput());
binaryWriter.Write(workbook);
binaryWriter.Close();
...
...

```




```VB.net

' Instantiate the ExcelService class.
Dim xlservice As New ExcelService()
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
Dim sheetName As String = "Sheet3"

' Set the path to the workbook to open.
' TODO: Change the path to the workbook
' to point to a workbook you have access to.
' The workbook must be in a trusted location.
' Call the open workbook, and point to the trusted 
' location of the workbook to open.
Dim targetWorkbookPath As String = http: String sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus) 'myserver02/example/Shared%20Documents/Book1.xlsx";

' Set the cell located in the first row and 
' ninth column to 300.
xlservice.SetCell(sessionId, sheetName, 0, 8, 300, outStatus)
xlservice.Refresh(sessionId, "MyInventoryConnection", outStatus)

Dim workbook() As Byte = xlService.GetWorkbook(sessionId, WorkbookType.FullWorkbook, status)

' Write the resulting Excel file to stdout 
' as a binary stream.
Dim binaryWriter As New BinaryWriter(Console.OpenStandardOutput())
binaryWriter.Write(workbook)
binaryWriter.Close()
...
...

```


## <a name="see-also"></a><span data-ttu-id="75cee-114">См. также</span><span class="sxs-lookup"><span data-stu-id="75cee-114">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="75cee-115">Задачи</span><span class="sxs-lookup"><span data-stu-id="75cee-115">Tasks</span></span>


  
    
    
 [<span data-ttu-id="75cee-116">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="75cee-116">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="75cee-117">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="75cee-117">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
  
    
    
 [<span data-ttu-id="75cee-118">How to: Get an Entire Workbook or a Snapshot</span><span class="sxs-lookup"><span data-stu-id="75cee-118">How to: Get an Entire Workbook or a Snapshot</span></span>](how-to-get-an-entire-workbook-or-a-snapshot.md)
#### <a name="concepts"></a><span data-ttu-id="75cee-119">Понятия</span><span class="sxs-lookup"><span data-stu-id="75cee-119">Concepts</span></span>


  
    
    
 [<span data-ttu-id="75cee-120">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="75cee-120">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="75cee-121">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="75cee-121">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="75cee-122">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="75cee-122">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="75cee-123">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="75cee-123">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="75cee-124">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="75cee-124">Other resources</span></span>


  
    
    
 [<span data-ttu-id="75cee-125">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="75cee-125">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
