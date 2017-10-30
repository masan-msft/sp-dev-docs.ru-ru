---
title: How to Save to the Server to Prepare for Programmatic Access
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 80b34a29-3d40-4d11-9ba1-b4886ffcfd42
ms.openlocfilehash: e17d155f2c67b957990a119cae8f7d2a2eb00049
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-save-to-the-server-to-prepare-for-programmatic-access"></a><span data-ttu-id="c1caa-103">How to: Save to the Server to Prepare for Programmatic Access</span><span class="sxs-lookup"><span data-stu-id="c1caa-103">How to: Save to the Server to Prepare for Programmatic Access</span></span>

<span data-ttu-id="c1caa-p101">This example shows how to save an Excel workbook to the server to to prepare it for programmatic access. The steps are:</span><span class="sxs-lookup"><span data-stu-id="c1caa-p101">This example shows how to save an Excel workbook to the server to to prepare it for programmatic access. The steps are:</span></span>
  
    
    


1. <span data-ttu-id="c1caa-106">Create a workbook with named ranges.</span><span class="sxs-lookup"><span data-stu-id="c1caa-106">Create a workbook with named ranges.</span></span>
    
  
2. <span data-ttu-id="c1caa-107">Save the workbook to a trusted SharePoint library location.</span><span class="sxs-lookup"><span data-stu-id="c1caa-107">Save the workbook to a trusted SharePoint library location.</span></span> 
    
    > <span data-ttu-id="c1caa-108">**Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения.</span><span class="sxs-lookup"><span data-stu-id="c1caa-108">**Note:** It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="c1caa-109">Дополнительные сведения можно [как: надежного расположения](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="c1caa-109">For more information, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
3. <span data-ttu-id="c1caa-p103">Programmatically specify values for the worksheet, named range, and cell value by using the Веб-службы Excel **SetCellA1** method. The values are passed in as argumentsthat is, _args [1]_ and _args [2]_:</span><span class="sxs-lookup"><span data-stu-id="c1caa-p103">Programmatically specify values for the worksheet, named range, and cell value by using the Excel Web Services **SetCellA1** method. The values are passed in as arguments—that is, _args [1]_ and _args [2]_:</span></span>
    
```cs
  
status = xlServices.SetCellA1(sessionId, String.Empty, args[1], args[2]);
```


```VB.net
  status = xlServices.SetCellA1(sessionId, String.Empty, args(1), args(2))
```


<span data-ttu-id="c1caa-112">You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:</span><span class="sxs-lookup"><span data-stu-id="c1caa-112">You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:</span></span>
  
    
    




```
GetSnapshot.exe http://MyServer002/MyTrustedDocumentLibrary/TestMyParam.xlsx MyParam28 > MySnapshot.xlsx 
```

<span data-ttu-id="c1caa-p104">In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="c1caa-p104">In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span></span>
### <a name="to-create-a-named-range"></a><span data-ttu-id="c1caa-115">To create a named range</span><span class="sxs-lookup"><span data-stu-id="c1caa-115">To create a named range</span></span>


1. <span data-ttu-id="c1caa-116">Start Excel.</span><span class="sxs-lookup"><span data-stu-id="c1caa-116">Start Excel.</span></span>
    
  
2. <span data-ttu-id="c1caa-117">Rename **Sheet1** to beMyParamSheet.</span><span class="sxs-lookup"><span data-stu-id="c1caa-117">Rename **Sheet1** to beMyParamSheet.</span></span>
    
  
3. <span data-ttu-id="c1caa-118">In cell B2, type 20.</span><span class="sxs-lookup"><span data-stu-id="c1caa-118">In cell B2, type 20.</span></span>
    
  
4. <span data-ttu-id="c1caa-119">In cell B3, type =2+B2.</span><span class="sxs-lookup"><span data-stu-id="c1caa-119">In cell B3, type =2+B2.</span></span>
    
  
5. <span data-ttu-id="c1caa-120">Make cell B3 bold.</span><span class="sxs-lookup"><span data-stu-id="c1caa-120">Make cell B3 bold.</span></span>
    
  
6. <span data-ttu-id="c1caa-121">Make cell B2 into a named range:</span><span class="sxs-lookup"><span data-stu-id="c1caa-121">Make cell B2 into a named range:</span></span> 
    
1. <span data-ttu-id="c1caa-122">On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.</span><span class="sxs-lookup"><span data-stu-id="c1caa-122">On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.</span></span>
    
  
2. <span data-ttu-id="c1caa-123">In the **Defined Names** group, click **Define Name**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-123">In the **Defined Names** group, click **Define Name**.</span></span>
    
  
3. <span data-ttu-id="c1caa-124">In the **New Name** dialog box, in the **Name** text box, typeMyParam.</span><span class="sxs-lookup"><span data-stu-id="c1caa-124">In the **New Name** dialog box, in the **Name** text box, typeMyParam.</span></span>
    
  
7. <span data-ttu-id="c1caa-p105">Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p105">Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx.</span></span> 
    
  

### <a name="to-save-to-a-sharepoint-library"></a><span data-ttu-id="c1caa-127">To save to a SharePoint library</span><span class="sxs-lookup"><span data-stu-id="c1caa-127">To save to a SharePoint library</span></span>


1. <span data-ttu-id="c1caa-128">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-128">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span></span> 
    
  
2. <span data-ttu-id="c1caa-129">In the **Save to SharePoint** dialog box, click **Publish Options**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-129">In the **Save to SharePoint** dialog box, click **Publish Options**.</span></span>
    
  
3. <span data-ttu-id="c1caa-130">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="c1caa-130">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="c1caa-131">Click **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-131">Click **Parameters**.</span></span> 
    
  
5. <span data-ttu-id="c1caa-132">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-132">Click **Add**.</span></span>
    
  
6. <span data-ttu-id="c1caa-p106">In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p106">In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.</span></span>
    
  
7. <span data-ttu-id="c1caa-p107">Click **OK**. You should now see **MyParam** in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p107">Click **OK**. You should now see **MyParam** in the **Parameters** list.</span></span>
    
  
8. <span data-ttu-id="c1caa-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-137">Click **OK**.</span></span>
    
  
9. <span data-ttu-id="c1caa-138">In the **Save to SharePoint** dialog box, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-138">In the **Save to SharePoint** dialog box, click **Save As**.</span></span>
    
  
10. <span data-ttu-id="c1caa-139">In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.</span><span class="sxs-lookup"><span data-stu-id="c1caa-139">In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.</span></span>
    
  
11. <span data-ttu-id="c1caa-p108">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p108">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.</span></span>
    
  
12. <span data-ttu-id="c1caa-142">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-142">Click **Save**.</span></span>
    
  

### <a name="to-specify-values-programmatically"></a><span data-ttu-id="c1caa-143">To specify values programmatically</span><span class="sxs-lookup"><span data-stu-id="c1caa-143">To specify values programmatically</span></span>


1. <span data-ttu-id="c1caa-144">Following is the signature for the **SetCellA1** method in Веб-службы Excel:</span><span class="sxs-lookup"><span data-stu-id="c1caa-144">Following is the signature for the **SetCellA1** method in Excel Web Services:</span></span>
    
```cs
  public void SetCellA1 (
string sessionId,
string sheetName,
string rangeName,
Object cellValue,
Out Status[] status
)
```


```VB.net
  
Public Sub SetCellA1(ByVal sessionId As String,
              ByVal sheetName As String, 
             ByVal rangeName As String, 
             ByVal cellValue As Object, 
             Out ByVal status() As Status)
End Sub
```


    Set the values for the worksheet, named range, and cell value to the **SetCellA1** method as follows:
    


```cs
  
// Set a value into a cell.
status = xlSrv.SetCellA1(sessionId, String.Empty, args[1], args[2]);

```

2. <span data-ttu-id="c1caa-145">In the preceding code:</span><span class="sxs-lookup"><span data-stu-id="c1caa-145">In the preceding code:</span></span> 
    
  -  <span data-ttu-id="c1caa-p109">_args [1]_ is the name of the named range. In this example, it is **MyParam**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p109">_args [1]_ is the name of the named range. In this example, it is **MyParam**.</span></span>
    
  
  -  <span data-ttu-id="c1caa-p110">_args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-p110">_args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.</span></span>
    
  
3. <span data-ttu-id="c1caa-150">If you are using a command line, you can pass in the arguments as follows:</span><span class="sxs-lookup"><span data-stu-id="c1caa-150">If you are using a command line, you can pass in the arguments as follows:</span></span>
    
     <span data-ttu-id="c1caa-151">`GetSnapshot.exe http://`_MyServer002_ `/` _MyTrustedDocumentLibrary_`/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`</span><span class="sxs-lookup"><span data-stu-id="c1caa-151">`GetSnapshot.exe http://` _MyServer002_ `/` _MyTrustedDocumentLibrary_ `/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`</span></span>
    
  
4. <span data-ttu-id="c1caa-152">If you generate a snapshot of the workbook, you see the following:</span><span class="sxs-lookup"><span data-stu-id="c1caa-152">If you generate a snapshot of the workbook, you see the following:</span></span> 
    
  - <span data-ttu-id="c1caa-153">Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-153">Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.</span></span>
    
  
  - <span data-ttu-id="c1caa-154">Cell B3 has a new calculated value of **30**.</span><span class="sxs-lookup"><span data-stu-id="c1caa-154">Cell B3 has a new calculated value of **30**.</span></span>
    
  
  - <span data-ttu-id="c1caa-155">Cell B3 does not show the original formula, which was "=2+B2".</span><span class="sxs-lookup"><span data-stu-id="c1caa-155">Cell B3 does not show the original formula, which was "=2+B2".</span></span>
    
  
  - <span data-ttu-id="c1caa-156">Cell B3 retains its font format, which is bold.</span><span class="sxs-lookup"><span data-stu-id="c1caa-156">Cell B3 retains its font format, which is bold.</span></span>
    
  

> <span data-ttu-id="c1caa-157">**Примечание:** Дополнительные сведения о моментальных снимков можно [как: получение всей книги или ее снимка](how-to-get-an-entire-workbook-or-a-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="c1caa-157">**Note:** For more information about snapshots, see  [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span></span> <span data-ttu-id="c1caa-158">Дополнительные сведения о методе **SetCellA1** веб-служб Excel см.</span><span class="sxs-lookup"><span data-stu-id="c1caa-158">For more information about the **SetCellA1** method, see the Excel Web Services reference documentation.</span></span> <span data-ttu-id="c1caa-159">Пространство имен веб-службы является [Microsoft.Office.Excel.Server.WebServices (en)](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c1caa-159">The namespace of the Web service is [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) .</span></span>
  
    
    


## <a name="see-also"></a><span data-ttu-id="c1caa-160">См. также</span><span class="sxs-lookup"><span data-stu-id="c1caa-160">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="c1caa-161">Задачи</span><span class="sxs-lookup"><span data-stu-id="c1caa-161">Tasks</span></span>


  
    
    
 [<span data-ttu-id="c1caa-162">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="c1caa-162">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
#### <a name="reference"></a><span data-ttu-id="c1caa-163">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="c1caa-163">Reference</span></span>


  
    
    
 [<span data-ttu-id="c1caa-164">Microsoft.Office.Excel.Server.WebServices</span><span class="sxs-lookup"><span data-stu-id="c1caa-164">Microsoft.Office.Excel.Server.WebServices</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx)
#### <a name="concepts"></a><span data-ttu-id="c1caa-165">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="c1caa-165">Concepts</span></span>


  
    
    
 [<span data-ttu-id="c1caa-166">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="c1caa-166">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="c1caa-167">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="c1caa-167">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [<span data-ttu-id="c1caa-168">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="c1caa-168">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="c1caa-169">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="c1caa-169">Other resources</span></span>


  
    
    
 [<span data-ttu-id="c1caa-170">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="c1caa-170">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
