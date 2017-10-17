---
title: "Оповещения для служб Excel"
ms.date: 09/25/2017
keywords: "ошибки"
f1_keywords: errors
ms.prod: sharepoint
ms.assetid: a4e7030b-05c2-484e-b21f-46cba937b803
ms.openlocfilehash: 044d7ee1f89cf16d567c8ae949eb58c0c9b2accd
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-alerts"></a><span data-ttu-id="067e0-103">Оповещения для служб Excel</span><span class="sxs-lookup"><span data-stu-id="067e0-103">Excel Services Alerts</span></span>

<span data-ttu-id="067e0-104">Веб-службы Excel exposes alerts for errors that occur within the Web service and errors that are returned by Службы вычислений Excel.</span><span class="sxs-lookup"><span data-stu-id="067e0-104">Excel Web Services exposes alerts for errors that occur within the Web service and errors that are returned by Excel Calculation Services.</span></span>
  
    
    

<span data-ttu-id="067e0-105">Errors are exposed in the following ways:</span><span class="sxs-lookup"><span data-stu-id="067e0-105">Errors are exposed in the following ways:</span></span>
- <span data-ttu-id="067e0-p101">Excel calculation errors are returned similarly to how they are shown in Excelthat is, as cell error values, such as #VALUE!. When you call the **GetCell** or **GetRange** methods and request formatted values, you will get the # style error string. If you request unformatted values, you will get an enumerated error code. For more information, see the [Error Codes](#excel-services-alerts_errorcodes) section later in this topic.</span><span class="sxs-lookup"><span data-stu-id="067e0-p101">Excel calculation errors are returned similarly to how they are shown in Excel—that is, as cell error values, such as #VALUE!. When you call the **GetCell** or **GetRange** methods and request formatted values, you will get the # style error string. If you request unformatted values, you will get an enumerated error code. For more information, see the [Error Codes](#excel-services-alerts_errorcodes) section later in this topic.</span></span>
    
  
- <span data-ttu-id="067e0-p102">When an error occurs during the processing of one of the Web service methods, preventing the method from finishing successfully, the error is exposed as a Simple Object Access Protocol (SOAP) exception. You can and should catch this error in your code. These types of errors are also known as "stop" alerts.</span><span class="sxs-lookup"><span data-stu-id="067e0-p102">When an error occurs during the processing of one of the Web service methods, preventing the method from finishing successfully, the error is exposed as a Simple Object Access Protocol (SOAP) exception. You can and should catch this error in your code. These types of errors are also known as "stop" alerts.</span></span>
    
  
- <span data-ttu-id="067e0-p103">Errors that do not prevent the method from returning normal results are returned as part of the method arguments, specifically as an output argument. These types of errors are considered non-critical errors. The reason the errors are returned as an output argument instead of an exception is because throwing an exception would divert the code from its normal execution path, which is not desirable with noncritical errors. Checking for these errors is optional. These types of errors are also known as "continue" alerts.</span><span class="sxs-lookup"><span data-stu-id="067e0-p103">Errors that do not prevent the method from returning normal results are returned as part of the method arguments, specifically as an output argument. These types of errors are considered non-critical errors. The reason the errors are returned as an output argument instead of an exception is because throwing an exception would divert the code from its normal execution path, which is not desirable with noncritical errors. Checking for these errors is optional. These types of errors are also known as "continue" alerts.</span></span>
    
  

## <a name="types-of-alerts"></a><span data-ttu-id="067e0-118">Types of Alerts</span><span class="sxs-lookup"><span data-stu-id="067e0-118">Types of Alerts</span></span>

<span data-ttu-id="067e0-119">There are two types of alerts: "stop" and "continue."</span><span class="sxs-lookup"><span data-stu-id="067e0-119">There are two types of alerts: "stop" and "continue."</span></span>
  
    
    

### <a name="stop-alerts"></a><span data-ttu-id="067e0-120">"stop" alerts</span><span class="sxs-lookup"><span data-stu-id="067e0-120">"stop" alerts</span></span>

<span data-ttu-id="067e0-p104">The "stop" alert causes the current operation to stop. This means the workbook will be rolled back to its state prior to execution of the current operation. The "stop" alerts are exposed as SOAP exceptions.</span><span class="sxs-lookup"><span data-stu-id="067e0-p104">The "stop" alert causes the current operation to stop. This means the workbook will be rolled back to its state prior to execution of the current operation. The "stop" alerts are exposed as SOAP exceptions.</span></span>
  
    
    

### <a name="continue-alerts"></a><span data-ttu-id="067e0-124">"continue" alerts</span><span class="sxs-lookup"><span data-stu-id="067e0-124">"continue" alerts</span></span>

<span data-ttu-id="067e0-p105">The "continue" alert is typically a warning or non-critical error. When Службы вычислений Excel throws a "continue" alert, the operation continues. These alerts are returned as out argumentsa struct with the various alert fields. For more information, see the **Status** class reference topics in the **Microsoft.Office.Excel.Server.WebServices** namespace.</span><span class="sxs-lookup"><span data-stu-id="067e0-p105">The "continue" alert is typically a warning or non-critical error. When Excel Calculation Services throws a "continue" alert, the operation continues. These alerts are returned as out arguments—a struct with the various alert fields. For more information, see the **Status** class reference topics in the **Microsoft.Office.Excel.Server.WebServices** namespace.</span></span>
  
    
    

## <a name="exceptions-to-catch"></a><span data-ttu-id="067e0-129">Exceptions to Catch</span><span class="sxs-lookup"><span data-stu-id="067e0-129">Exceptions to Catch</span></span>

<span data-ttu-id="067e0-p106">You should catch errors specific to Службы вычислений Excel that you know the user might cause. For example, if your application prompts the user to type the path to a workbook, the user might type the wrong path or select a workbook that does not exist. You cannot control what the user types, but you can control the user experience when a user unintentionally misspells a workbook file name.</span><span class="sxs-lookup"><span data-stu-id="067e0-p106">You should catch errors specific to Excel Calculation Services that you know the user might cause. For example, if your application prompts the user to type the path to a workbook, the user might type the wrong path or select a workbook that does not exist. You cannot control what the user types, but you can control the user experience when a user unintentionally misspells a workbook file name.</span></span>
  
    
    
<span data-ttu-id="067e0-p107">You should catch the SOAP exceptions (that is, "stop" alerts) in your code. For "continue" alerts, the calling code may choose to ignore or review the alert information.</span><span class="sxs-lookup"><span data-stu-id="067e0-p107">You should catch the SOAP exceptions (that is, "stop" alerts) in your code. For "continue" alerts, the calling code may choose to ignore or review the alert information.</span></span>
  
    
    

## <a name="error-codes"></a><span data-ttu-id="067e0-135">Коды ошибок</span><span class="sxs-lookup"><span data-stu-id="067e0-135">Error Codes</span></span>
<span data-ttu-id="067e0-136"><a name="excel-services-alerts_errorcodes"> </a></span><span class="sxs-lookup"><span data-stu-id="067e0-136"><a name="excel-services-alerts_errorcodes"> </a></span></span>

<span data-ttu-id="067e0-p108">To enable catching specific error conditions, an Службы вычислений Excel alert has an associated error code. The web service then returns the error using properties from the **SoapException** class.</span><span class="sxs-lookup"><span data-stu-id="067e0-p108">To enable catching specific error conditions, an Excel Calculation Services alert has an associated error code. The web service then returns the error using properties from the **SoapException** class.</span></span>
  
    
    
<span data-ttu-id="067e0-139">For more information, see the "SoapException Class" topic in the Microsoft .NET Framework SDK documentation.</span><span class="sxs-lookup"><span data-stu-id="067e0-139">For more information, see the "SoapException Class" topic in the Microsoft .NET Framework SDK documentation.</span></span>
  
    
    

## <a name="exception-handling"></a><span data-ttu-id="067e0-140">Exception Handling</span><span class="sxs-lookup"><span data-stu-id="067e0-140">Exception Handling</span></span>
<span data-ttu-id="067e0-141"><a name="excel-services-alerts_errorcodes"> </a></span><span class="sxs-lookup"><span data-stu-id="067e0-141"><a name="excel-services-alerts_errorcodes"> </a></span></span>

<span data-ttu-id="067e0-p109">If your application (that is, your SOAP client) sends a request to a web service that the service is unable to process, the service returns a SOAP exception to the client. Handling exceptions thrown by Веб-службы Excel is an important part of the applications that you develop, because you can return specific information to users when errors occur. Exception handling can also help improve the user experience when something unexpected happens in your application.</span><span class="sxs-lookup"><span data-stu-id="067e0-p109">If your application (that is, your SOAP client) sends a request to a web service that the service is unable to process, the service returns a SOAP exception to the client. Handling exceptions thrown by Excel Web Services is an important part of the applications that you develop, because you can return specific information to users when errors occur. Exception handling can also help improve the user experience when something unexpected happens in your application.</span></span>
  
    
    
<span data-ttu-id="067e0-145">For general information about exception handling, see "Handling and Throwing Exceptions" in the Microsoft .NET Framework SDK documentation.</span><span class="sxs-lookup"><span data-stu-id="067e0-145">For general information about exception handling, see "Handling and Throwing Exceptions" in the Microsoft .NET Framework SDK documentation.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="067e0-146">См. также</span><span class="sxs-lookup"><span data-stu-id="067e0-146">See also</span></span>
<span data-ttu-id="067e0-147"><a name="excel-services-alerts_errorcodes"> </a></span><span class="sxs-lookup"><span data-stu-id="067e0-147"><a name="excel-services-alerts_errorcodes"> </a></span></span>


#### <a name="concepts"></a><span data-ttu-id="067e0-148">Понятия</span><span class="sxs-lookup"><span data-stu-id="067e0-148">Concepts</span></span>


  
    
    
 [<span data-ttu-id="067e0-149">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="067e0-149">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="067e0-150">Коды ошибок для служб Excel</span><span class="sxs-lookup"><span data-stu-id="067e0-150">Excel Services Error Codes</span></span>](excel-services-error-codes.md)
#### <a name="other-resources"></a><span data-ttu-id="067e0-151">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="067e0-151">Other resources</span></span>


  
    
    
 [<span data-ttu-id="067e0-152">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="067e0-152">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="067e0-153">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="067e0-153">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="067e0-154">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="067e0-154">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
