---
title: "Этап 3. Получение доступа к веб-службе"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d27f654d-242f-4f34-8385-be857c170532
ms.openlocfilehash: be159956d3799a2c9dac2d3aef309a178889f494
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-3-accessing-the-web-service"></a>Этап 3. Получение доступа к веб-службе

Следующим этапом после добавления ссылки на веб-службы Веб-службы Excel в проект является создание экземпляра прокси-класса веб-службы. Затем можно будет получить доступ к методам веб-службы путем вызова методов в прокси-классе. Когда приложение вызывает эти методы, код прокси-класса созданный Visual Studio, обрабатывает обмен данными между приложением и веб-службой. 
  
    
    

Сначала требуется создать экземпляр прокси-класса веб-службы ExcelWebService. Затем с помощью прокси-класса выполняется вызов различных методов и свойств веб-службы. Такие вызовы используются для открытия книги, получения кода сеанса, предъявления стандартных учетных данных, определения объекта координат диапазона, получения диапазона, использующего объект координат диапазона, закрытия книги и перехвата исключений SOAP.
  
    
    


## <a name="accessing-the-web-service"></a>Получение доступа к веб-службе


### <a name="to-add-directives"></a>Добавление директив


1. При добавлении веб-ссылки в более ранних версий он создан объект с именем ExcelService в пространство имен с именем <yourProject>. <webReferenceName>. В этом примере объект с именем SampleApplication.ExcelWebService. В этом пошаговом руководстве также показано, как для перехвата исключений SOAP. Чтобы сделать это, используйте объект **System.Web.Services.Protocols** . Пространство имен **System.Web.Services.Protocols** состоит из классов, определяющих протоколы, используемые для передачи данных по сети между клиентами веб-службы и веб-служб XML с помощью ASP.NET.
  
    
    
Для упрощения использования этих объектов необходимо сначала добавить пространства имен в качестве директив в файл Class1.cs. В этом случае при использовании таких директив не требуется указывать полные имена типов в пространстве имен. 
    
  
2. Для добавления таких директив добавьте следующий код в начало собственного кода в файле Class1.cs после элемента  `using System:`
    
```cs
  
using SampleApplication.ExcelWebService;
using System.Web.Services.Protocols;
```


```VB.net
  
Imports SampleApplication.ExcelWebService
Imports System.Web.Services.Protocols
```


### <a name="to-call-the-web-service"></a>Вызов веб-службы


1. Выполните создание экземпляра и инициализацию прокси-объекта веб-службы путем добавления следующего кода после открывающей скобки в строке  `static void Main(string[] args)`:
    
```cs
  
ExcelService es = new ExcelService();
```


```VB.net
  Dim es As New ExcelService()
```

2. Для создания массива состояний и объектов координат диапазона добавьте следующий код:
    
```cs
  Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
```


```VB.net
  
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
```

3. Добавьте код, чтобы указать лист, к которому требуется получить доступ. В этом примере лист называется Sheet1. Добавьте в свой код следующее: 
    
```cs
  
string sheetName = "Sheet1";
```


```VB.net
  Dim sheetName As String = "Sheet1"
```


    > **Note:**
      > Make sure the workbook you want to open has a worksheet called "Sheet1" that contains values. Alternatively, you can change "Sheet1" in the code to the name of your worksheet. 
4.  `Add the following code to point to the workbook you want to open`:
    
```cs
  string targetWorkbookPath = "http://myserver02/example/Shared%20Documents/Book1.xlsx";
```


```VB.net
  Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"
```


    > **Important:**
      > Change the workbook path to match the location of the workbook you are using for this walkthrough. Make sure the workbook exists and that the location where the workbook is saved is a trusted location. Using an HTTP URL to point to the location of a workbook allows you to access it remotely. 

    > **Note:**
      > You can get the path to a workbook in Microsoft SharePoint Server 2010 by right-clicking the workbook and selecting **Copy Shortcut**. Alternatively, you can select **Properties** and copy the path to the workbook from there.
5. Добавьте следующий код, чтобы указать учетные данные для запроса. 
    
    > **Примечание:** Необходимо явно задать учетные данные, даже в том случае, если вы намерены использовать учетные данные по умолчанию. 

```cs
  es.Credentials = System.Net.CredentialCache.DefaultCredentials;
```


```VB.net
  es.Credentials = System.Net.CredentialCache.DefaultCredentials
```

6. Добавьте следующий код, чтобы открыть книгу и указать надежное расположение, где размещается эта книга. Поместите код в блок **try**:
    
```cs
  try
{
string sessionId = es.OpenWorkbook(targetWorkbookPath, "en-US", 
    "en-US", out outStatus);
```


```VB.net
  
Try
Dim sessionId As String = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
```

7. Добавьте следующий код, чтобы подготовить объект для определения координат диапазона и вызвать метод **GetRange**. Код также выполнит печать общего количества строк в диапазоне и значений в конкретном диапазоне.
    
```cs
  
rangeCoordinates.Column = 3;
rangeCoordinates.Row = 9;
rangeCoordinates.Height = 18;
rangeCoordinates.Width = 12;

object[] rangeResult1 = es.GetRange(sessionId, sheetName,
    rangeCoordinates, false, out outStatus);
Console.WriteLine("Total rows in range: " + rangeResult1.Length);
Console.WriteLine("Value in range is: " + ((object[])rangeResult1[5])[2]);
```


```VB.net
  
rangeCoordinates.Column = 3
rangeCoordinates.Row = 9
rangeCoordinates.Height = 18
rangeCoordinates.Width = 12

Dim rangeResult1() As Object = es.GetRange(sessionId, sheetName, rangeCoordinates, False, outStatus)
Console.WriteLine("Total rows in range: " &amp; rangeResult1.Length)
Console.WriteLine("Value in range is: " &amp; (CType(rangeResult1(5), Object()))(2))
```

8. Добавьте код, чтобы закрыть рабочую книгу и завершить текущий сеанс. Затем добавьте закрывающую скобку в конце блока **try**.
    
    > **Важные:** Рекомендуется закрыть книгу, если вы выполнили к сеансу. Это приведет к закрытию сеанса и освобождения ресурсов. 

```cs
  
es.CloseWorkbook(sessionId);
}
```


```VB.net
  
es.CloseWorkbook(sessionId)
```

9. Добавьте блок **catch** для перехвата исключений SOAP и печати сообщения об исключении:
    
```cs
  catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As SoapException
    Console.WriteLine("SOAP Exception Message: {0}", e.Message)
End Try
```


## <a name="complete-code"></a>Полный пример кода

Приведенный ниже пример кода представляет собой полный фрагмент кода в файле примера Class1.cs, который описывается выше.
  
    
    

> **Важные:** Вносить изменения в путь к книге, имя листа и т. д соответствующим образом. 
  
    
    


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
            // Instantiate the Web service and create a status array object and range coordinate object
            ExcelService es = new ExcelService();
            Status[] outStatus;
            RangeCoordinates rangeCoordinates = new RangeCoordinates();
            
string sheetName = "Sheet1";
            // Using workbookPath this way will allow 
            // you to call the workbook remotely.
            // TODO: change the workbook path to 
            // point to workbook in a trusted location
            // that you have access to 
            string targetWorkbookPath = "http://myserver02/example/Shared%20Documents/Book1.xlsx";
//you can also use .xlsb files, for example, //"http://myserver02/example/Shared%20Documents/Book1.xlsb";

            // Set credentials for requests
            es.Credentials = System.Net.CredentialCache.DefaultCredentials;
            //Console.WriteLine("Cred: {0}", es.Credentials);
            try
            {
                // Call open workbook, and point to the trusted   
                // location of the workbook to open.
                string sessionId = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);
                // Console.WriteLine("sessionID : {0}", sessionId);

                // Prepare object to define range coordinates
                // and the GetRange method.
                rangeCoordinates.Column = 3;
                rangeCoordinates.Row = 9;
                rangeCoordinates.Height = 18;
                rangeCoordinates.Width = 12;

                object[] rangeResult1 = es.GetRange(sessionId, sheetName, rangeCoordinates, false, out outStatus);
                Console.WriteLine("Total Rows in Range: " + rangeResult1.Length);
                Console.WriteLine("Value in range is: " + ((object[])rangeResult1[5])[3]); 
        
                // Close workbook. This also closes session.
                es.CloseWorkbook(sessionId);
            }
            catch (SoapException e)
            {
                Console.WriteLine("SOAP Exception Message: {0}", e.Message);
            }
            // catch (Exception e)
//            {
//                Console.WriteLine("Exception Message: {0}", e.Message);
//            }
//            Console.ReadLine();
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
            ' Instantiate the Web service and create a status array object and range coordinate object
            Dim es As New ExcelService()
            Dim outStatus() As Status
            Dim rangeCoordinates As New RangeCoordinates()

Dim sheetName As String = "Sheet1"
            ' Using workbookPath this way will allow 
            ' you to call the workbook remotely.
            ' TODO: change the workbook path to 
            ' point to workbook in a trusted location
            ' that you have access to 
            Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"
'you can also use .xlsb files, for example, //"http://myserver02/example/Shared%20Documents/Book1.xlsb";

            ' Set credentials for requests
            es.Credentials = System.Net.CredentialCache.DefaultCredentials
            'Console.WriteLine("Cred: {0}", es.Credentials);
            Try
                ' Call open workbook, and point to the trusted   
                ' location of the workbook to open.
                Dim sessionId As String = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
                ' Console.WriteLine("sessionID : {0}", sessionId)

                ' Prepare object to define range coordinates
                ' and the GetRange method.
                rangeCoordinates.Column = 3
                rangeCoordinates.Row = 9
                rangeCoordinates.Height = 18
                rangeCoordinates.Width = 12

                Dim rangeResult1() As Object = es.GetRange(sessionId, sheetName, rangeCoordinates, False, outStatus)
                Console.WriteLine("Total Rows in Range: " &amp; rangeResult1.Length)
                Console.WriteLine("Value in range is: " &amp; (CType(rangeResult1(5), Object()))(3))

                ' Close workbook. This also closes session.
                es.CloseWorkbook(sessionId)
            Catch e As SoapException
                Console.WriteLine("SOAP Exception Message: {0}", e.Message)
            ' Catch e As Exception
            '    Console.WriteLine("Exception Message: {0}", e.Message)
            End Try
            'Console.ReadLine()
        End Sub
    End Class
End Namespace
```


## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Шаг 1. Создание проекта клиента веб-службы](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Этап 2. Добавление веб-ссылки](step-2-adding-a-web-reference.md)
  
    
    
 [Этап 4. Построение и тестирование приложения](step-4-building-and-testing-the-application.md)
  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
