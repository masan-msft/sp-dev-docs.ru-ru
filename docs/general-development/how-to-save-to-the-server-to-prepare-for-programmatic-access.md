---
title: "Сохранение на сервере для подготовки для программного доступа"
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 80b34a29-3d40-4d11-9ba1-b4886ffcfd42
ms.openlocfilehash: 32162a764919dc313bd1d64e9867029ba7ffb8ee
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="save-to-the-server-to-prepare-for-programmatic-access"></a>Сохранение на сервере для подготовки для программного доступа

В этом примере показано, как сохранить книгу Excel на сервере для подготовки для программного доступа. Порядок действий:

1. Create a workbook with named ranges.
    
  
2. Save the workbook to a trusted SharePoint library location. 
    
    > **Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения. Дополнительные сведения можно [как: надежного расположения](how-to-trust-a-location.md). 
3. Programmatically specify values for the worksheet, named range, and cell value by using the Веб-службы Excel **SetCellA1** method. The values are passed in as argumentsthat is, _args [1]_ and _args [2]_:
    
```cs
  
status = xlServices.SetCellA1(sessionId, String.Empty, args[1], args[2]);
```


```VB.net
  status = xlServices.SetCellA1(sessionId, String.Empty, args(1), args(2))
```


You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:
  
    
    




```
GetSnapshot.exe http://MyServer002/MyTrustedDocumentLibrary/TestMyParam.xlsx MyParam28 > MySnapshot.xlsx 
```

In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).
### <a name="to-create-a-named-range"></a>To create a named range


1. Start Excel.
    
  
2. Rename **Sheet1** to beMyParamSheet.
    
  
3. In cell B2, type 20.
    
  
4. In cell B3, type =2+B2.
    
  
5. Make cell B3 bold.
    
  
6. Make cell B2 into a named range: 
    
1. On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.
    
  
2. In the **Defined Names** group, click **Define Name**.
    
  
3. In the **New Name** dialog box, in the **Name** text box, typeMyParam.
    
  
7. Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx. 
    
  

### <a name="to-save-to-a-sharepoint-library"></a>To save to a SharePoint library


1. On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**. 
    
  
2. In the **Save to SharePoint** dialog box, click **Publish Options**.
    
  
3. In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.
    
  
4. Click **Parameters**. 
    
  
5. Click **Add**.
    
  
6. In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.
    
  
7. Click **OK**. You should now see **MyParam** in the **Parameters** list.
    
  
8. Click **OK**.
    
  
9. In the **Save to SharePoint** dialog box, click **Save As**.
    
  
10. In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.
    
  
11. In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.
    
  
12. Click **Save**.
    
  

### <a name="to-specify-values-programmatically"></a>To specify values programmatically


1. Following is the signature for the **SetCellA1** method in Веб-службы Excel:
    
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

2. In the preceding code: 
    
  -  _args [1]_ is the name of the named range. In this example, it is **MyParam**.
    
  
  -  _args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.
    
  
3. If you are using a command line, you can pass in the arguments as follows:
    
     `GetSnapshot.exe http://`_MyServer002_ `/` _MyTrustedDocumentLibrary_`/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`
    
  
4. If you generate a snapshot of the workbook, you see the following: 
    
  - Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.
    
  
  - Cell B3 has a new calculated value of **30**.
    
  
  - Cell B3 does not show the original formula, which was "=2+B2".
    
  
  - Cell B3 retains its font format, which is bold.
    
  

> **Примечание.** Дополнительные сведения о снимках см. в статье [Инструкции. Получение всей книги или моментального снимка](how-to-get-an-entire-workbook-or-a-snapshot.md). Дополнительные сведения о методе **SetCellA1** веб-служб Excel см. Пространство имен веб-службы является [Microsoft.Office.Excel.Server.WebServices (en)](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) .
  
    
    


## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [How to: Save from Excel Client to the Server](how-to-save-from-excel-client-to-the-server.md)
#### <a name="reference"></a>Справочные материалы


  
    
    
 [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api.md)
  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
